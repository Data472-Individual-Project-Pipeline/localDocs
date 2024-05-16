# Deploy serverless application

- Install Docker Desktop in your laptop
    - Check if WSL 2 is Enabled
    - Open PowerShell as Administrator
        - `wsl --list --verbose`
        - If you see "Version 2" next to your listed distributions, you are set.
            
            ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled.png)
            
    - docker run hello-world
        
        ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled%201.png)
        
- Install AWS CLI on Windows
    
    Download the **AWS CLI installer** for Windows from the [AWS CLI official page](https://aws.amazon.com/cli/).
    
    From powershell:
    
    ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled%202.png)
    
- Install AWS SAM CLI on Windows
    
    Windows Installer (MSI) files are the package installer files for the Windows operating system.
    
    Download and install the AWS SAM CLI using the MSI file [64-bit](https://github.com/aws/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_64_PY3.msi).
    
    ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled%203.png)
    
- Configure AWS
    - create a new access-key in IAM and save secret accesskey
    
    ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled%204.png)
    
- App
    - > sam init
        
        ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled%205.png)
        
    - > cd sam-app
    - >  sam build
        
        ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled%206.png)
        
    
    To test locally:
    
    - >  sam local invoke
        
        ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled%207.png)
        
    
    To deploy to cloud:
    
    - > sam deploy --guided
        
        ![Untitled](Deploy%20serverless%20application%200dd42220d1d04081a4a0295a3381405b/Untitled%208.png)