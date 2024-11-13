WordPress-Hosting
Hosting WordPress on an AWS EC2 Instance

This guide will walk you through hosting a WordPress website on AWS EC2, covering all essential steps from creating an account to configuring the server for WordPress. Follow each step below to complete the setup.

Prerequisites
An AWS account with access to EC2 services.
Basic familiarity with command-line operations.
Steps
Step 1: Create an AWS Account
Sign up for an AWS account if you don't already have one.
Step 2: Launch an EC2 Instance
Go to the EC2 dashboard on AWS.
Launch a new EC2 instance with Ubuntu (or any Linux-based AMI).
Configure the instance's security groups to allow HTTP (port 80) and SSH (port 22) access.
Step 3: Connect to Your EC2 Instance
Use SSH to access your instance:
bash
Copy code
ssh -i /path/to/your-key.pem ubuntu@your-ec2-public-ip
Step 4: Install and Configure Dependencies
1. Update & Upgrade the Server
bash
Copy code
sudo apt update && sudo apt upgrade
2. Install Apache Web Server
bash
Copy code
sudo apt install apache2
Check Apache Status:
bash
Copy code
sudo systemctl status apache2
3. Install PHP
bash
Copy code
sudo apt install php php-mysql php-gd php-cli php-common
4. Install MariaDB (MySQL Alternative)
bash
Copy code
sudo apt install mariadb-server mariadb-client
Secure MariaDB Installation:
bash
Copy code
sudo mysql_secure_installation
Respond to the prompts:
Enter current password: Press Enter for none
Set up options as follows: n, n, y, y, y, y
5. Create a Database and User for WordPress
Open MariaDB:
bash
Copy code
sudo mysql -u root -p
Create Database:
sql
Copy code
CREATE DATABASE DATABASENAME;
Create User and Set Password:
sql
Copy code
CREATE USER 'USERNAME'@'localhost' IDENTIFIED BY 'PASSWORD';
Grant Privileges:
sql
Copy code
GRANT ALL PRIVILEGES ON DATABASENAME.* TO 'USERNAME'@'localhost';
Exit MariaDB:
sql
Copy code
exit
6. Download and Configure WordPress
Download WordPress:
bash
Copy code
sudo wget https://wordpress.org/latest.tar.gz -P /var/www/html/
Extract WordPress:
bash
Copy code
sudo tar -xvzf /var/www/html/latest.tar.gz -C /var/www/html/
Set Permissions:
bash
Copy code
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress
7. Configure Apache for WordPress
Edit Apache Config File:
bash
Copy code
sudo nano /etc/apache2/sites-available/000-default.conf
Set DocumentRoot: Find the DocumentRoot line and update it:
apache
Copy code
DocumentRoot /var/www/html/wordpress/
Enable Apache Rewrite Module:
bash
Copy code
sudo a2enmod rewrite
8. Restart Apache
bash
Copy code
sudo systemctl restart apache2
Check Apache Status:
bash
Copy code
sudo systemctl status apache2
Step 5: Complete WordPress Setup
Open your browser and go to http://your-ec2-public-ip.
Follow the on-screen instructions to complete the WordPress installation.
Troubleshooting
If you encounter any issues, try the following:

Check if Apache is running: sudo systemctl status apache2.
Ensure the EC2 instance's security group allows HTTP and SSH access.
Verify MariaDB service is active: sudo systemctl status mariadb.
