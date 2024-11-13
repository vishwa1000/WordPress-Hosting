# WordPress-Hosting
Hosting wordpress in AWS EC2

Update CMT
		-> sudo apt update 
		
		
upgrade CMT 
		-> sudo apt upgrade 
		
		
Apache Install CMT: 
		-> sudo apt install apache2 
		
		
Status of the application CMT: 
		-> sudo systemctl status apache2 


PHP Install CMT:
		-> sudo apt install php php-mysql php-gd php-cli php-common

Maria DB Install CMT: 
		-> sudo apt install mariadb-server mariadb-client


MYSQL Installation CMT: 
		-> sudo mysql_secure_installation
			-> press enter 
			-> no
			-> no
			-> yes
			-> yes
			-> yes
			-> yes

Database & User Creation CMT: 
		-> sudo mysql -u root -p


Database create CMT: 
		-> create database DATABASENAME;

		
User & Password Creation CMT: 
		-> create user 'USERNAME'@'localhost' identified by 'PASSWORD';


to check user is created or not:
		-> SELECT User  FROM mysql.user;


Privileges Set CMT: 
		-> grant all privileges on DATABASENAME.* to "USERNAME"@"localhost";


exit out of MariaDB:
		-> exit

Copy CMT: 
		-> sudo cp -r [FOLDERNAME]

Download the latest version of WordPress inside /var/www/html/:
		->sudo wget https://wordpress.org/latest.tar.gz


unzipping wordpress:
		-> sudo tar -xvzf latest.tar.gz



Apche2 Config. file Directory CMT: 
		-> cd /etc/apache2/sites-available


open file 000-default.conf:
		-> sudo nano 000-default.conf


Find the "000-default.conf" need to open the file and change the HTML Directory
		-> DocumentRoot /var/www/html/wordpress/


Permissions on wordpress file needs to be changed:
		-> sudo chown -R www-data:www-data /var/www/html/wordpress
		-> sudo chmod -R 755 /var/www/html/wordpress


Enable Apache Rewrite Module:
		-> sudo a2enmod rewrite



Restart Apache:
		-> sudo systemctl restart apache2



Check Apache Status:
		-> sudo systemctl status apache2
