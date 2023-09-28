# 🚀 Automated WordPress Deployment with Nginx, LEMP Stack, and GitHub Actions

_**This repository contains all the necessary code and configuration files
to set up an automated deployment process for a WordPress website using
Nginx as the web server, LEMP (Linux, Nginx, MySQL, PHP) stack, and
GitHub Actions as the CI/CD automation tool, triggered whenever commits are pushed to the master branch or manually triggered using the "workflow_dispatch" event.
The deployment process follows security best practices and ensures optimal performance of the
website.**_

🌐 **Deployed Website URL:** [https://cloudpresshub.ddns.net](https://cloudpresshub.ddns.net)

![CloudPressHub](/ReadMeImages/CloudPressHub.png)

## Table of Contents

- [Server Provisioning](#-server-provisioning)
- [Nginx, MySQL/MariaDB, and PHP Setup](#-nginx-mysqlmariadb-and-php-setup)
- [WordPress Website Configuration](#-wordpress-website-configuration)
- [GitHub Repository Setup](#-github-repository-setup)
- [GitHub Actions Workflow](#-github-actions-workflow)
  - [Fork or Clone This Repository](#1-fork-or-clone-this-repository)
  - [Configure GitHub Secrets 🤐](#2-configure-github-secrets-)
  - [Configure WordPress (if applicable)](#3-configure-wordpress-if-applicable)
  - [Customize the Workflow (Optional)](#4-customize-the-workflow-optional)
  - [Push to Master Branch 🎆](#5-push-to-master-branch-)
  - [Monitor Deployment](#6-monitor-deployment)
- [Welcome New Contributors Workflow 👋](#welcome-new-contributors-workflow-)


## Prerequisites

Before you begin, make sure you have the following prerequisites in place:

- **Cloud Server**: You will need access to a Virtual Private Server (VPS) from a major cloud provider like AWS, Azure, Google Cloud, or DigitalOcean.

- **GitHub Account**: You need a GitHub account for version control and collaboration. If you don't have one, you can sign up for free at [GitHub](https://github.com/).

- **Site Domain**: You can register a domain of your choice or use a temporary domain/IP-based URL. Alternatively, you can use free domain names from [noip.com](https://www.noip.com/).

Now, let's dive into the setup and deployment process step by step.

## 🛠️ Server Provisioning

Let's start by getting our server up and running on AWS (or your cloud provider of choice). Here's the plan:

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

    ```bash
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

This workflow is designed to be super-easy to integrate into your own WordPress project or any other PHP-based project. 

## Getting Started 🚀

### 1. Fork or Clone This Repository

You've got two options: fork this repository if you want to make it your own, or simply clone it directly into your local environment.

```bash
# Clone this repository
git clone https://github.com/TasneemHegazy/CloudPressHub-Deploy.git
```

### 2. Configure GitHub Secrets 🤐

In your repository settings, head over to the "Secrets" section and sprinkle in these secrets:

- `MYSQL_ROOT_PASSWORD`: Your MySQL root password.
- `MYSQL_USER`: Your MySQL username.
- `MYSQL_PASSWORD`: Your MySQL password.
- `MYSQL_DATABASE`: Your MySQL database name.
- `MYSQL_HOST`: MySQL host (default: 127.0.0.1).
- `REMOTE_TARGET`: Remote target directory for deployment.
- `HOSTNAME`: Hostname for the remote server.
- `REMOTE_USER`: Remote server username.
- `SSH_PRIVATE_KEY`: SSH private key for the secret handshake.
- `SLACK_WEBHOOK`: Slack webhook URL for notifications.

### 3. Configure WordPress (if applicable)

If you're using this workflow for a WordPress project, set up your WordPress instance as needed.

### 4. Customize the Workflow (Optional)

You can customize the workflow defined in `.github/workflows/deployment.yml` to match your project's unique style. Adjust PHP versions, coding standards, or deployment settings.

### 5. Push to Master Branch 🎆

With everything set up, push your changes to the master branch. This will trigger the CD workflow automatically.

```bash
# Push your changes
git push origin master
```

### 6. Monitor Deployment

Head to the "Actions" tab in your GitHub repository to monitor the workflow in action. You'll see details of each workflow run, and if anything comes up, the workflow will let you know!

## Welcome New Contributors Workflow

This repository also includes a workflow to welcome new contributors when they open new issues or pull requests. You can use this workflow as is, or customize it to suit your project's welcome message.

Whenever new issues or pull requests are opened, the workflow will send a welcome message to contributors.

Feel free to explore the workflows in this repository, adapt them to your specific project requirements, and make the most of automated deployments and contributor engagement.


## Welcome New Contributors Workflow 👋

This repository also includes a workflow to welcome new contributors when they open new issues or pull requests. 
Whenever new issues or pull requests are opened, the workflow will send a welcome message to your contributors. 💌

Feel free to explore, customize, and make these workflows your own, and make the most of automated deployments and contributor engagement! 😄✨




