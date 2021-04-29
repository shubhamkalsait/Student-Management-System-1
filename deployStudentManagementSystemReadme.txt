***Student-Management-System-by-AmirHamza***
Steps to deploy Application

Step1: Install and configure LAMP server
	# apt update -y
	# apt-get install apache2 mariadb-server php -y
	# apt-get install libapache2-mod-php php-mysql -y
	# vim /etc/apache2/mods-enabled/dir.conf
			bring index.php at front
	# systemctl start apache2 mariadb
	# systemctl enable apache2 mariadb
	# mysql_secure_installation
	
Step2: Prepare mysql for remote login
	# vim /etc/mysql/mariadb.conf.d/50-server.cnf 
		OR
	# vim /etc/mysql/my.cnf
	
			bind-address = 0.0.0.0
			
Step3: Create remote user and database
	# mysql -u root -p
		mysql> create database cloudblitz;
		mysql> create user radmin@'%' identified by 'remoteuserpwd';
		mysql> grant all privileges on *.* to radmin@'%';
		mysql> flush privileges;

Step4: Allow firewall port if firewall is active
	# ufw allow http
	# ufw allow mysql
	
Step5: Clone repository https://github.com/amirhamza05/Student-Management-System.git 
	and move all files at /var/www/html

Step6: Add below lines in 'config/db.php'
   <?php
                define('db_host', 'ec2-65-0-184-99.ap-south-1.compute.amazonaws.com');
                define('db_user', 'radmin');
                define('db_pass', 'remoteuserpwd');
                define('db_name', 'cloudblitz');
        ?>

Try Login using user:admin  password:admin


