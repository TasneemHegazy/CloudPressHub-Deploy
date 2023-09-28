# 🚀 Automated WordPress Deployment with Nginx, LEMP Stack, and GitHub Actions

[![Continuous Deployment Workflow](https://github.com/TasneemHegazy/CloudPressHub-Deploy/actions/workflows/deployment.yml/badge.svg)](https://github.com/TasneemHegazy/CloudPressHub-Deploy/actions/workflows/deployment.yml)

_**Hey there! 👋😄 This repository represents a state-of-the-art implementation of CI/CD for a WordPress website, powered by the LEMP (Linux, Nginx, MySQL, PHP) stack, and streamlined by GitHub Actions. This GitHub Actions workflow automates the continuous integration and deployment (CI/CD) process. while following best practices for security, performance, and automation.**_

## Tech Stack 🛠️

- **Web Server:** I'm using Nginx web server, carefully configured for optimum website performance. Below are some of the optimizations I've implemented:

   - **Caching:** I've added caching to make my website lightning-fast.

   - **Gzip Compression:** Data gets a shrink-wrap treatment for faster transmission.

- **Database:** MySQL/MariaDB ensures robust data management for my WordPress website, ensuring it runs smoothly.

- **Hosting:** I host my website on AWS EC2 instances, providing scalability and reliability.

- **SSL/TLS Encryption:** Secure communication between my server and clients is guaranteed through Let's Encrypt SSL/TLS certificates.

- **Domain Names:** I utilize free domain names from [noip.com](https://www.noip.com/) to give my website a professional online identity.

- **CI/CD Automation:** GitHub Actions is my CI/CD automation tool of choice, ensuring seamless and efficient deployment and making life easier.

## Features 🌟

- **Enhanced Security:** I follow industry best practices to ensure the highest level of security for your WordPress website, like strong passwords and limited user access. 

- **Automated Deployment:** My GitHub Actions workflow handles the automated deployment of my WordPress website to my AWS EC2 instances.

- **Dependency Management:** I cache Composer dependencies to speed up future runs and run PHP Code Sniffer to maintain code quality. Any fixes suggested by PHP Code Sniffer are automatically committed.

- **Slack Integration:** Receive real-time updates on my project's status by sending messages to a designated Slack channel. I'll be instantly informed in case of job failures.

- **Contributor Engagement:** I also have a workflow in place to welcome new contributors when they open new issues or pull requests. Building a collaborative community is a priority.

🌐 **Deployed Website URL:** [https://cloudpresshub.ddns.net](https://cloudpresshub.ddns.net)

![CloudPressHub](/ReadMeImages/CloudPressHub.png)

## Table of Contents

- [Prerequisites](#prerequisites)
- [Server Provisioning](#-server-provisioning)
- [Nginx, MySQL/MariaDB, and PHP Setup](#-nginx-mysqlmariadb-and-php-setup)
- [WordPress Website Configuration](#-wordpress-website-configuration)
- [GitHub Repository Setup](#github-repository-setup)
- [GitHub Actions Workflow](#-github-actions-workflow)
   - [Workflow Overview](#workflow-overview)
   - [How to Use](#how-to-use)
     - [1. Fork or Clone This Repository](#1-fork-or-clone-this-repository)
     - [2. Configure Secrets 🤐](#2-configure-github-secrets-)
     - [3. Workflow Trigger](#3-workflow-trigger)
     - [4. Customize Environment Configuration](#4-customize-the-workflow-optional)
     - [5. Save the Workflow](#5-save-the-workflow)
     - [6. Manual Production Deployment](#6-manual-production-deployment)
     - [7. Monitor Deployment](#7-monitor-deployment)
- [Welcome New Contributors Workflow 👋](#welcome-new-contributors-workflow-)

## Prerequisites

Before you begin, make sure you have the following prerequisites in place:

- **Cloud Server**: You will need access to a Virtual Private Server (VPS) from a major cloud provider like AWS, Azure, Google Cloud, or DigitalOcean.

- **GitHub Account**: You need a GitHub account for version control and collaboration. If you don't have one, you can sign up for free at [GitHub](https://github.com/).

- **Site Domain**: You can register a domain of your choice or use a temporary domain/IP-based URL. Alternatively, you can use free domain names from [noip.com](https://www.noip.com/).

Now, let's dive into the setup and deployment process step by step.

## 🛠️ Server Provisioning

Let's start by getting my server up and running on AWS (or your cloud provider of choice). Here's the plan:

-   Provision an EC2 instance on AWS with a secure Linux distribution
    (e.g., Ubuntu 22.04).

-   Configure security groups to allow necessary incoming trafficand be a bit strict with unnecessary access.

-   Generate and configure SSH key pairs for secure remote access...

## 💻 Nginx, MySQL/MariaDB, and PHP Setup

-   Install and configure Nginx as the web server.

   ```bash
   sudo apt update

   sudo apt install nginx

   sudo systemctl start nginx

   sudo systemctl enable nginx
   ```
-   Set up MySQL/MariaDB as the database and configure it securely.

   ```bash
   sudo apt install mysql-server

   sudo systemctl start mysql

   sudo systemctl enable mysql
      
   sudo mysql_secure_installation
   ```

   Follow the prompts to set a root password and secure your MySQL installation.

-   Install and configure PHP for processing dynamic content.

```bash
sudo yum install php php-mysqlnd php-fpm -y

sudo systemctl start php-fpm

sudo systemctl enable php-fpm
```
## 🌐 WordPress Website Configuration
-   Access your EC2 instance and set up a WordPress website.

-   Navigate to your Nginx web server root directory.

```bash
cd /var/www/html/
   ```

-   Download and Extract WordPress:
   
   ```bash
   sudo wget https://wordpress.org/latest.tar.gz
   sudo tar -xzvf latest.tar.gz
   ```

-   Set Permissions:
    
    ```bash
    sudo chown -R www-data:www-data /var/www/html/wordpress
    sudo chmod -R 755 /var/www/html/wordpress
    ```

-   Create a MySQL Database and User:

    Access MySQL with root privileges:
    
    ```bash
    sudo mysql -u root -p
    ```

    Create a WordPress database, user, and grant privileges:
    
    ```sql
    CREATE DATABASE wordpress;
    CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;
    ```

-   Configure WordPress:
    
    Rename the WordPress sample configuration file and edit it:

    ```bash
    cp /var/www/html/wordpress/wp-config-sample.php /var/www/html/wordpress/wp-config.php
    sudo nano /var/www/html/wordpress/wp-config.php
    ```

    Update the database details with the database name, username, and password you created earlier.

-   WordPress Website Setup:
    
    Open your web browser and access your server's domaster name or IP address. Follow the WordPress setup wizard to complete the installation.

-   Secure Your WordPress Installation: 🔒
    
    After installation, follow best practices for WordPress security. This includes strong passwords, limiting user privileges, and keeping plugins and themes up to date.

-   Implement SSL/TLS certificate using Let\'s Encrypt for secure
    communication.

## **GitHub Repository Setup**

-   Create a GitHub repository for this project.

   On your server, navigate to your WordPress project directory:

    cd /var/www/html/wordpress

    # Initialize a Git repository

    git init

    # Add and Commit Files

    git add .
    git commit -m "Initial commit"

-   Link to Your GitHub Repository:
    
    Go back to GitHub, and you'll find a URL for your repository. Link your local repository to GitHub by following the instructions on the GitHub website.


```bash

git remote add origin  your-github-repo-url.git

git branch -M master

git push -u origin master
```

-   files pushed from the ec2 instances to the git repository

- Your WordPress site should now be running on your server, and your code is version-controlled in your GitHub repository. You can push updates to GitHub whenever you make changes to your site.

## 🛠️ GitHub Actions Workflow

This workflow is designed to be super-easy to integrate into your own WordPress project or any other PHP-based project. It's designed to ensure code quality and deploy changes to both staging and production environments from the master branch.

## Workflow Overview

1. **PHP Coding Standards Check (PHPCS)**
   - Runs PHP Code Sniffer to enforce coding standards.
   - Utilizes a MySQL service for database-related checks.
   - Caches Composer dependencies for faster subsequent runs.

2. **Deploy to Staging**
   - Deploys the application to the staging environment.
   - Uses rsync to transfer files securely to the staging server.

3. **Deploy to Production (Manual)**
   - **Note:** Production deployment is configured for manual approval.
   - To deploy to production, follow these steps:
     - Review the changes in the production environment.
     - Approve the deployment.
     - Manually trigger the production deployment workflow.

4. **Slack Notification**
   - Sends a notification to a Slack channel upon successful deployment to staging or production.

## How to Use

To implement this CI/CD workflow, follow these steps:

### 1. Fork or Clone This Repository

You've got two options: fork this repository if you want to make it your own, or simply clone it directly into your local environment.

```bash
# Clone this repository
git clone https://github.com/TasneemHegazy/CloudPressHub-Deploy.git
```

### 2. Configure Secrets 🤐

Ensure that you have set up the required secrets in your GitHub repository for the following environments:

- **Staging Environment:**
  - `STAGING_TARGET`: The target path on the staging server where files should be deployed.
  - `STAGING_HOSTNAME`: The hostname or IP address of the staging server.
  - `STAGING_REMOTE_USER`: The SSH username for accessing the staging server.
  - `STAGING_SSH_PRIVATE_KEY`: The private SSH key for authentication to the staging server.

- **Production Environment:**
  - `PRODUCTION_TARGET`: The target path on the production server where files should be deployed.
  - `PRODUCTION_HOSTNAME`: The hostname or IP address of the production server.
  - `PRODUCTION_REMOTE_USER`: The SSH username for accessing the production server.
  - `PRODUCTION_SSH_PRIVATE_KEY`: The private SSH key for authentication to the production server.

- **Database Configuration:**
  - `MYSQL_ROOT_PASSWORD`: The MySQL root password for database-related checks.
  - `MYSQL_USER`: The MySQL username for database-related checks.
  - `MYSQL_PASSWORD`: The MySQL password for database-related checks.
  - `MYSQL_DATABASE`: The name of the MySQL database for database-related checks.

- **Slack Notification:**
  - `SLACK_WEBHOOK`: The Slack webhook URL for sending deployment notifications.

### 3. Workflow Trigger

This workflow is triggered automatically on pushes to the master branch or can be manually triggered using the "workflow_dispatch" event.

### 4. Customize Environment Configuration

Modify the configuration in the workflow as needed to match your project's requirements. You can add additional steps, tests, or deployment actions to suit your specific needs.

### 5. Save the Workflow

Save this workflow configuration as a `.github/workflows/deployment.yml` file in your repository.

### 6. Manual Production Deployment

Production deployment is configured for manual approval. To deploy to production:

1. Review the changes in the production environment.
![Ask to Review Production](/ReadMeImages/ask-review-production.png)
2. Approve the deployment.
![Manual Production Deployment](/ReadMeImages/ApproveAndDeploy.png)
3. Manually trigger the production deployment workflow.
![Successful Production Deployment](/ReadMeImages/deployed-production.png)


### 7. Monitor Deployment

Head to the "Actions" tab in your GitHub repository to monitor the workflow in action. You'll see details of each workflow run, and if anything comes up, the workflow will let you know!

## Welcome New Contributors Workflow 👋

This repository also includes a workflow to welcome new contributors when they open new issues or pull requests. 
Whenever new issues or pull requests are opened, the workflow will send a welcome message to your contributors. 💌

_**Feel free to explore, customize, and make these workflows your own, and make the most of automated deployments and contributor engagement! 😄✨**_




