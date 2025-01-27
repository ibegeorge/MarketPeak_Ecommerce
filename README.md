# Project Directory Creation
I started this project by first creating an empty directory called MarketPeak_Ecommerce and initialised git in it 
```bash
    mkdir MarketPeak_Ecommerce
    cd MarketPeak_Ecommerce
    git init
```
I downloaded the necessary website template files from the recommended source - [Template](https://www.tooplate.com/view/2130-waso-strategy)
It downloaded as a zipped file and so I extracted it into the MarketPeak_Ecommerce directory that I used created 

Now I have the website files that I need, I didn't make any changes at this point to any of the files but the entire project folder
should have recorded a change as it is now being tracked by git.

I added the new files to staging area , to stage them for a commit and then linking my local repository with my github account by running these commands:
```bash
    git add .
    git config --global user.name "ibegeorge"
    git config --global user.email "nnanaibe@outlook.com"
    git commit -m "Initial commit with the basic e-commerce structure"
```
Then I went on my github account and created a new repository named "MarketPeak_Ecommerce" initialising it with a ReadMefile
I linked the local repository to my github repository by running the command : 
```bash
  git remote add origin https://github.com/ibegeorge/MarketPeak_Ecommerce.git
```
Finally for this section I uploaded the local repository to GitHub
```bash
   git checkout -b main
   git push -u origin main 
```
---
# AWS Deployment
I walked through deploying on AWS by setting up an Amazon Linux EC2 Instance as required 
1. Log in to AWS Management Console
2. Search EC2 on the search bar
3. Launch EC2 instance with accurate configurations and specifications ( Make sure to choose free tier and make proper security group settings to allow for https viewing )
4. Connect to the Instance via ssh

## Cloning my github repository on my Linux EC2 server/instance
Firstly, make sure git is installed on the machine. Run these on the Linux terminal to install
```bash
   sudo yum update -y
   sudo yum install git -y 
```
Then , On the Github account, I selected the MarketPeak_Ecommerce repo and then clicked the Code Dropdown Button to select a clone method.
My preferred choice is HTTPS, so I select HTTPs and Copied the HTTPS URL for cloning
Back to my Linux terminal I run git clone + the Https URl like so
```bash
   git clone https://github.com/ibegeorge/MarketPeak_Ecommerce.git
```
I am prompted for username and password which I enter and Now I have my project folder on my Amazon Linux server.

## Installation of Apache Web Server (httpd) on Amazon Linux Server
I ran the following commands on my Amazon Linux terminal to install , start and enable Apache (httpd)
```bash
   sudo yum update -y
   sudo yum install httpd -y
   sudo systemctl start httpd
   sudo systemctl enable httpd
```
## Configuring httpd to serve my website
By default httpd has a folder where it has its own files that it serves up located in the html folder
> var/www/html/

In order to serve my own website related files I empty out the html folder, then copy and paste my website related files into it.
That is, Copy and Paste all contents of the MarketPeak_Ecommerce folder into 'html' folder. 
```bash
   sudo rm -rf /var/www/html/*
   sudo cp -r ~/MarketPeak_Ecommerce/* var/www/html/
```
Now I reload the Apache(httpd) server to have it load with the recent changes 
```bash
   sudo systemctl reload httpd
```
---
# Access Website from Browser

In order to ascertain that everything works correctly , I have to test it with a browser. I do this by copying the Public IP address of my Amazon Linux EC2 and paste that in a browser
It works, loads up the Ecommerce website!

---

# Continued Development
For continued development, I made a change to the index.html file of this project. 
Now on the terminal , while in the MarketPeak_Ecommerece directory, I run
```bash
   nano index.html
```
and make changes on the file, although not much was changed. 
I created a new branch called development and switched to it in other to stage the files for commit and further push to github
```bash
   git checkout -b development
   git add .
   git commit -m "made change on the index.html"
   git push -u origin development
```
---
# Merge Development branch with main branch on Github
Finally, on github I created a Pull Request for the development branch and then Merged it with the main branch after checking to see that there were no conflicts.
