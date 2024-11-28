
# **E-Commerce Platform Deployment With Git, Linux and AWS**

## **Implement Version Control with GIT**
* Create a repository named MarketPeak_Ecommerce `mkdir MareketPeak_Ecommerce`
* Inside this directory,Initialize a GIT repository with `git init` command
![](./img/GITINIT.png)

* Download and add the website files to the Git repository
![](./img/GPwebsite%20template.png)
* Set Git global configuration with your username and password. You can set it with this command 

    `git config --global user.name "Your Name"`

    `git config --global user.name "email"`

    Confirm the username and email is set with command below

     `git config --global --list`
    ![](./img/Gituserandpass.png)

* Stage and Commit changes with clear and descriptive message
![](./img/Gitcommit.png)
* Push the codes to GitHub repository

      Firstly,create a remote repository named `MarketPeak_Ecommerce`.Leave the repository empty without initializing with README, gitignore or Licence.
      
     
  ![](./img/GITHUB%20REPO.png)
  Next,Link the local repository to GitHub : git remote add origin

  `git remote add origin https://github.com/Edward-okoto/MarketPeak_Ecommerce.git`
    ![](./img/GITRemote-V.png)

    To push the codes to GitHub, run command 

    `git push -u origin main`
    ![](./img/Gitpush.png)
    The push command enable us to push the our commit from the local main branch to the remote GitHub repository,enabling us to store our projects in the cloud and share with others.

    local repo files/directory has been pushed to GitHub
    ![](./img/Gitremote-result.png)

   ## **AWS Deployment**
    ### Setting up an AWS EC2 instance

  * Log in to the AWS management console 
  * Launch an EC2 instance using an Amazon Linux AMI
  ![](./img/EC2.png)
  * Connect to the instance using SSH

    Click instance ID
  ![](./img/ServerRunning.png)
  Copy the public Ip address
  ![](./img/PublickIPAddress.png)
  Go to mobaxterm terminal, click new session,input the Ip address,default username is `ec2-user` and add the key generated(downloaded) on your local machine when instance was created.
  ![](./img/mobaxterm.png)




  #### Clone the `MarketPeak_Ecommerce` Repository on the Linux Server.
  * On GitHub copy the SSH code
  ![](./img/SSHcodeCopy.png)
  * Generate SSH keypair on EC2 instance using `ssh-keygen`
  ![](./img/keygen2.png)
  * Display and copy the key

     `cat /home/ec2-user/.ssh/id_rsa`
  * Add the public SSH key to GitHUB account
    Go to GitHub, click settings, click SSH and GPG keys
    ![](./img/SETTINGS.png)
  * click `New SSH key` and add the public key
    ![](./img/New%20SSH%20key.png)
  * Use the SSH code to clone the repository
  ![](./img/Clone.png)
  ![](./img/LScomm.png)

  ## Install WebServer on EC2

    * Install Apache Http server
  
      `sudo yum update -y`

      `sudo yum install httpd -y`

      `sudo systemctl start httpd`

      `sudo systemctl enable httpd`

      ![](./img/httpdONE.png)
  ### Configure httpd for Website
    * **Prepare the web directory**: Clear the default httpd web directory and copy the MarkerPeak_Ecommerce fies into it.

           sudo rm -rf /var/www/html/*

          sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
    * **Reload httpd**:Apply the changes by reloading httpd.

          sudo systemctl reload httpd

 Access Website from Browser

    Use the public ip and the path to the http server files to browse to the website.  `http://16.171.63.100/TrinityTekeme/okoto`
![](./img/WEBSITE.Trinity.png)

### **Continuous Integration and Deployment Workflow**
* Develop new features and fixes

   Procedure: 
   
   * **Create a `Development Branch`** and begin work from there to isolate new features and bug fixes from the stable version of the website.

     `git branch Development`
   ![](./img/GIT%20DEVbranch.png)

   * **Implement changes**: 
    
      Starter-page.html was updated to reflect new Template name and version
   * **Stage Changes**
     
     `git add .`
      ![](./img/DEVgitADD.png)
   * **Commit the changes**   
     `git commit -m 'Template name and version updated`
      ![](./img/DEVGitcommit.png)
   * **Push changes to GitHub**

     `git push origin Development`
      ![](./img/DEVgitPush.png)
   * **Create a PR and Merge**
   ![](./img/PullRequest.png)
   * **Deploy updates to the production Server and Test changes**

     * Pull the latest changes from GitHUB to the webserver

     `git pull origin main`
     ![](./img/Gitpull.png)

     * Test the changes


     ![](./img/FINAL.png)


# **Key Challange**

* **Problems Encountered**: Website didnt work even after configuration was double-checked.

* **Solution** : Allow HTTP traffic on port 80 in the inbound Security Group for the EC2 instance.

   

