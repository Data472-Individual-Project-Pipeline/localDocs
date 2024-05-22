# localDocs
Local Documentation

# Table of contents.
Setting up AWS < You are here <br>

[Set a Shiny App](SettingUpaShinyApponEC2example.md)

Learn how to set up a shiny app for the first time.

[Git Workflow](GitWorkflow.md)

Learn how to use git more efficiently

[Set up your first flask application](flaskappdeployec2example.md)

Learn how to deploy a popular python web framework called Flask.



# How do i install AWS Client and docker?
Install Docker Desktop (https://docs.docker.com/desktop/install/windows-install/)

On an EC2 instance running Ubuntu (https://docs.docker.com/engine/install/ubuntu)

# Set up and installation of AWS CLI
## ACCESS KEY
>[!IMPORTANT]
>Please read all of the instructions carefully! <br/> If you are unsure do not proceed without asking for assistance.
>Your access key will be used to connect to your account when using AWS CLI and AWS SAM CLI.

# Generaing AWS Access and Secret Key
This can be achieved by accessing your aws Security Credentials,
![Menu popdown](image.png)

This is done under your Security Credentials, the menu can be accessed using the top right of your console, located by clicking on username@uc-research-gdr-poc, if you do not have a page open you can go to it here: <br>
https://uc-research-gdr-poc.signin.aws.amazon.com/console/
log in and access your Security Credentials.

you can add a description but the tag may error out, ignore this.

When you access your password (show)... This password will only be shown once.

>[!NOTE]
>You will not be able to recover your password, so do not lose it under any circumstances!

# AWS CLI Installation
Assuming you have linux.
```sh
# curl is used to collect the package, unzip is used to extract. Zip might be required for lambda packaging and misc aws functions.
sudo apt-get update && sudo apt-get install curl unzip zip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
## Update the CLI.
Only if you have AWS CLI already installed.
```sh
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
```

Make sure you run aws configure.
you can have multiple profiles by using this command
```sh
aws configure profile=profilename
```
How do i change profiles?
in the target console your AWS CLI and SAM CLI are installed on, assuming the profile has been configured you can export it two ways.
```sh
export AWS_PROFILE=profilename
```
The second way. 
locate your aws configuration file, typically it is located in
├── config <- you are here first
└── credentials <- edit this second
```sh
/home/username/.aws/config
```
And add the following on a new line below the last entry.
```conf
[profile mydodgysetup]
region = ap-southeast-2
output = json
```
We are not done yet!
Secondly in credentials
```conf
[mydodgysetup]
aws_access_key_id = test <- replace with the id from the security credential 
aws_secret_access_key = test <- replace with the key from the security credential
```
>[!IMPORTANT]
Your id and key must be from the same credential.
The profile name in both config and credentials need to match (aws configure does this for you.) <br>
**Make sure to check the profile you are in incase the changes you make affect another aws profile you also have pre-loaded**

>[!Additional Documentation]
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

# Install AWS SAM CLI
Assuming you have installed AWS CLI.

```sh
curl https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-linux-x86_64.zip -o aws-sam-cli-linux-x86_64.zip
unzip aws-sam-cli-linux-x86_64.zip -d sam-installation
sudo ./sam-installation/install
```

>[!Additional Documentation]
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html

Here's a guide to using AWS CLI with the hello-world lambda function.

4.	https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-getting-started-hello-world.html

This was done under linux

```sam init```

Select 1 (Hello World Example) then Python 3.12 or whatever suits you

Use defaults for everything else (just press enter.)

```cd sam-app```
```sam build```

For testing locally:

```sam local invoke```

Edit code in:
sam-app/hello_world/app.py

Add python packages to requirements.txt

To deploy to cloud:

```sam deploy --guided```

Use defaults (just press enter.)
