# localDocs
Local Documentation

# How do i install AWS Client and docker?
Install Docker Desktop (https://docs.docker.com/desktop/install/windows-install/)

On an EC2 instance running Ubuntu (https://docs.docker.com/engine/install/ubuntu)

# Set up and installation of AWS CLI
## ACCESS KEY
>Please read all of the instructions carefully! <br/> If you are unsure do not proceed without asking for assistance.

Your access key will be used to connect to your account when using AWS CLI and AWS SAM CLI.

1. Generate AWS Access Key and Secret
This is done under your Security Credentials, the menu is top right where the aws console displays username@uc-research-gdr-poc, if you do not have a page open you can go to it here: <br>
https://uc-research-gdr-poc.signin.aws.amazon.com/console/
log in and access your Security Credentials.

you can add a description but the tag may error out, ignore this.

When you access your password (show)... This password will only be shown once.
>You will not be able to recover your password, so do not lose it under any circumstances!

2.	Install AWS CLI
Found here <br>
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

3.	Install AWS SAM CLI
Found here <br>
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
