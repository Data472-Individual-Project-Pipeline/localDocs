# Setting Up a Shiny App on AWS EC2 with Data Fetching

### **Overview**

This documentation outlines the steps to set up a Shiny application on an AWS EC2 instance. The Shiny app will dynamically fetch JSON data from a public URL and display it in a data table.

### **Prerequisites**

- AWS EC2 instance running Ubuntu
- SSH access to the EC2 instance
- R and Shiny Server installed
- Public URL providing JSON-formatted data

### **Step-by-Step Guide**

**1. Launch an EC2 Instance**

1. Log in to the AWS Management Console.
2. Launch a new EC2 instance using Ubuntu as the operating system.
3. Configure security groups to allow traffic on port 3838 (default for Shiny Server).

**2. Connect to the EC2 Instance**

```bash
ssh -i /path/to/your-key.pem ubuntu@your-ec2-instance-public-ip
```

**3. Install R and Shiny Server**

Update package lists and install R:

```bash
sudo apt-get update
sudo apt-get install -y r-base

```

Install Shiny Server:

```bash
sudo su - -c "R -e \"install.packages('shiny', repos='http://cran.rstudio.com/')\""
sudo apt-get install -y gdebi-core
wget https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-1.5.14.948-amd64.deb
sudo gdebi shiny-server-1.5.14.948-amd64.deb
```

### **4. Install Required R Packages**

```bash
sudo su - -c "R"
```

Inside the R session:

```r
install.packages("shiny")
install.packages("httr")
install.packages("jsonlite")
install.packages("DT")
q()
```

### **5. Configure Shiny Server**

Edit the Shiny Server configuration file to ensure logging and correct app hosting:

```
sudo nano /etc/shiny-server/shiny-server.conf
```

Ensure the configuration includes:

```bash
# Instruct Shiny Server to run applications as the user "shiny"
run_as shiny;

# Define a server that listens on port 3838
server {
  listen 3838;

  # Define a location at the base URL
  location / {

    # Host the directory of Shiny Apps stored in this directory
    site_dir /srv/shiny-server;

    # Log all Shiny output to files in this directory
    log_dir /var/log/shiny-server;

    # When a user visits the base URL rather than a particular application,
    # an index of the applications available in this directory will be shown.
    directory_index on;
  }
}
```

Create the log directory and set permissions:

```bash

sudo mkdir -p /var/log/shiny-server
sudo chown shiny:shiny /var/log/shiny-server
sudo chmod 755 /var/log/shiny-server
```

Restart Shiny Server:

```bash
sudo systemctl restart shiny-server
sudo systemctl status shiny-server
sudo systemctl enable shiny-server
```

### **6. Deploy the Shiny App**

Create and place the Shiny app files in the appropriate directory:

```bash
sudo mkdir -p /srv/shiny-server/udc_app
sudo chown -R shiny:shiny /srv/shiny-server/udc_app
```

**ui.R:**

```r

library(shiny)

shinyUI(fluidPage(
  titlePanel("Urban Data Center - Data Viewer"),
  sidebarLayout(
    sidebarPanel(
      selectInput("dataset", "Choose a dataset URL:", 
                  choices = list("Dataset 1" = "http://13.211.113.178/data")),
      actionButton("loadData", "Load Data")
    ),
    mainPanel(
      DT::dataTableOutput("dataTable")
    )
  )
))

```

**server.R:**

```r
library(shiny)
library(httr)
library(jsonlite)
library(DT)

shinyServer(function(input, output, session) {
  observeEvent(input$loadData, {
    req(input$dataset)
    tryCatch({
      data <- GET(input$dataset)
      if (status_code(data) != 200) {
        stop("Failed to fetch data from URL. Status code: ", status_code(data))
      }
      data_content <- content(data, "text")
      data_json <- fromJSON(data_content)
      output$dataTable <- DT::renderDataTable({
        datatable(data_json)
      })
    }, error = function(e) {
      showNotification(paste("Error: ", e$message), type = "error")
      message(paste("Error: ", e$message))
    })
  })
})

```

### **7. Access the Shiny App**

Open a web browser and navigate to:

```
http://your-ec2-instance-public-ip:3838/udc_app
```

### **8. Monitor Logs for Errors**

If you encounter any issues, check the Shiny Server logs:

```
sudo tail -f /var/log/shiny-server/shiny-server.log

```

Or check system logs for more details:

```
sudo journalctl -u shiny-server -e

```

### **Conclusion**

By following these steps, you can successfully set up a Shiny application on an AWS EC2 instance to fetch and display JSON data from a public URL. This documentation should help you replicate the setup and troubleshoot any issues that arise during the process.