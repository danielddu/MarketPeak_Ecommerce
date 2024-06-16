
  ![Peak (3)](https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/ed78f149-1ffa-42f9-b9b9-7c627f742b48)


# E-Commerce Platform Deployment with Git, Linux, and AWS

Development of an e-commerce website for a new online marketplace named "MarketPeak." This platform
will feature product listings, a shopping cart, and user authentication. The objective is to utilize Git for version control, develop
the platform in a Linux environment, and deploy it on an AWS EC2 instance.

## Initialized Git Repository

I created a project directory named MarketPeak_Ecommerce by using `mkdir MarketPeak_Ecommerce`
Changed to the directory with `cd MarketPeak_Ecommerce`

Initiated git using `git init`

<img width="540" alt="1 gitinit" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/bfd020e8-a13f-43ad-8f29-317c6b80922b">

## Obtained and Prepare the E-commerce Website Template

Downloaded a pre-existing e-commere website template and made few adjustment to it. 

I customized the template to tailor it to "MarketPeak" to fit an e-commerce brand identity.

<img width="629" alt="marketpeak" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/9a6bea38-f0d3-446c-b4dc-f1b7b173db29">

## Staged and Committed the Template to Git

The website files were added to the Git repository by running `git add .`

Git global onfiguration was set up using `git config --global user.name danieddu` and `git config --global user.email tosindaudu87@gmail.com` 

<img width="457" alt="3 git-remote-add" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/9766ea79-8e5c-4a73-bec8-80ea4eb755d8">

Git commit was done with `git commit -m "Initial commit with basic e-commerce site structure"`

<img width="557" alt="2 gitcommit" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/25f604ab-35fe-4f28-8dc1-004e29ed2e9a">

## Git push to Repository

After initiating Git repository and adding the e-commerce website template, I pushed my code to the remote git repository. This step is crucial for version control and collaboration as it shares my local changes and publishes it to a public repository making them accessible to others.  

My local repository was linked to Github use the command, `git remote add origin https://github.com/danieddu/MarketPeak_Ecommerce.git`

And then pushed using `git push -u origin main`

<img width="453" alt="4 gitpush" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/e2383bdf-0d32-486a-a4fc-8fd8afeea5e0">

## AWS EC2 Instance Set Up 

Logged into my AWS Management console and lauched an EC2 instance using an Amazon Linux AMI.
I then coonected to the instance using SSH.

<img width="695" alt="5 connctinstance" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/9ec8d5fb-19df-4213-b169-168e18134c09">

## Cloned Repository on the Linux Server
Before the deployment of my e-commerce platform was done, I cloned the Github repository to my AWS EC2 instance. This process involves authenticating with Github and choosing between two primary methods of cloning a repository: `SSH` and `HTTPS`


On my EC2 instance, i generated SSH keypair using ssh-keygen

<img width="549" alt="7 sshkeygen" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/5612974a-61f4-4e97-a23f-4e4ee6e55386">

<img width="492" alt="8 sshkeygen" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/e8342261-3cf9-418e-bd0b-27de53661b19">

I then displayed and copied my public key by using the command, `cat /home/ubuntu/.ssh/id_rsa.pub`

<img width="584" alt="9 sshkey" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/f7569f06-de9c-4cef-a813-238f37cc1876">


The SSH key was used to clone the url

`git clone git@github.com:yourusername/MarketPeak_Ecommerce.git`

<img width="515" alt="10 gitclone" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/714921e1-2dba-461f-b968-e4a29ec83710">

## Installed Web Server on EC2

Apache Web Server which is known as httpd,  was installed on the EC2 instance. 
Apache Web Server (httpd) is a widely used web server that serves HTML files and content over the internet. Installing it on Linux EC2 allows me to host MarketPeak_Ecommerce website. 

I ran this script to achieve that. 
`sudo yum update -y`
`sudo yum install httpd -y`
`sudo systemctl start httpd`
`sudo systemctl enable httpd`


<img width="647" alt="11 sudo-yum-install" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/41411266-9263-4fa1-8af0-3132d21f6f97">

<img width="936" alt="12 sudo-yum-install-httpd" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/bac077e0-6226-4c17-b5dc-8f78be05231d">


This first updates the linux server and then installs httpd (Apache), starts the web server, and ensures it automatically starts on server boot. 


<img width="841" alt="19 sudo-systemctl-start-httpd" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/df1246b6-25e1-4619-abde-ec1cfe428941">

## Configured httpd for the Website

I configured httpd to point to the directory on the Linux server where the website code files are stored, usually in `/var/www/html`
This is done to serve the website from the EC2 instance. 
The directory `/var/www/html` is a standard directory structure on Linux systems that host website contents, particularly for the Apache HTTP Server. 



I first cleared the default httpd web directory and copied MarketPeak Ecommerce website files into it using the script, 
`sudo rm -rf /var/www/html/*`
`sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/`


<img width="614" alt="20 sudo-MarketPeak" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/ba17899f-4edd-4cef-8d06-2ed68a0fc8ec">

http was reloaded to apply the changes using the command `sudo systemctl reload httpd`


<img width="565" alt="21 sudo-reload-httpd" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/d1ecb386-512f-4a55-8f52-9c530522c52f">

With httpd configured and website files in place, MarketPeak Ecommerce platform is now live on the internet. 

<img width="629" alt="marketpeak" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/ab37a79d-6024-467c-8111-c6832298ba8e">


## Continious Integration and Deployment Workflow

To ensure a smooth workflow for developing, testing, and deploying my e-commerce platform, i folowed a structural approach. This normally involves making changes in a development environment, utilizing version control with Git, and deploying updates to production server on AWS. 

Step 1: Created a Development Branch. This isolated new features and bug fixes from the stable version of the websites.

I created this branch by running the following commands, 
`git branch development`
`git checkout development`

<img width="453" alt="13 git-branch-dev" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/844a1728-63fa-409b-9a4a-bab40ca5e154">

To implement a change, i changed the prices of some products on the website.

Step 2: I did version control with Git by staging my changes with `git add .`and commited the changes with a commmit message using `git commit -m "Changed product price`

<img width="532" alt="14 git-add-branch-dev" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/b1fd17dd-abe9-4bc2-b062-3e1500e824f4">

<img width="579" alt="15 git-commit-branch-dev" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/3eaa7fbb-9cce-4e89-ade1-201ff6d1fd3a">

I pushed changed to Github. This enables collaboration and version tracking. 
I did that by running the command, `git push origin development`

<img width="500" alt="16 git-push-origin-dev" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/30e11260-09f1-419d-aa21-ed7fddcd1a89">


Step 3: Pull Request and Merging to the Main branch. 
Created a Pull Request to merge the development branch into the main branch. This process is crucial for code review and maintaining code quality. 
Reviewed the changes for any potential issues. Once satisfied, I merged the pull request into the main branch, incorporating the product price change.

To do that, i ran the following commands, 
`git checkout main`
`git merge development`


<img width="747" alt="17 commit-change-gui" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/17c1513e-887f-455e-b7c0-19817e26307b">
<img width="957" alt="18 pull-request" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/e5a9e9b6-ac4d-4cf5-bd80-ab4e21bd3eee">
<img width="673" alt="20 merge-pull" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/edcdca63-ce74-47a5-920f-672beb69d3a5">


I then pushed the merged changes to Github by running `git push origin main` 

<img width="457" alt="24 git-pull-origin-main" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/04c48d12-1163-4916-b8cf-27361ad504cc">


Step 4: Deployed Updates to the Production Server
Pulled the latest changes on the server. SSH into AWS EC2 instance where the production website is hosted. Navigated to the websites's directory and pull the latest changes from the main branch by running command `git pull origin main`

<img width="679" alt="23 merge-successful" src="https://github.com/danielddu/MarketPeak_Ecommerce/assets/169099038/9046a0ad-9c64-4547-95f9-198fb6e1cd5a">

The web server was restarted to apply changes.
`sudo systemctl reload httpd` 

Step 5: Testing the New changes
Website was access using the public IP address on my EC2 instance. The new change in product price worked as expected. 








 












