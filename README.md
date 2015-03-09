# frog_website_all
Thanks for Monica https://github.com/wqr619/frog_website_all

# frog_website
Frog Online Test Website

# Introductions
#-----------------------------------------------------------------------------
Frog is a platform for automatic software testing. It helps to locate potential bugs by 3 simple steps

1. Upload source code, then test suites with will be generated and replayed automatically.

2. Specify test case replay result: Pass or Fail

3. Visualize potential bug locations in source code

Frog now supports C program testing.
URL: www.frog-test.com

# Installation Instructions
#---------------------------------------------------------------------------

# Step0 : download source
	$ sudo cd /var/www
	$ sudo git clone https://github.com/wqr619/frog_website_all.git .

# Step1 : Install/Configure LAMP (Web Developement Software)
	#**1.1 Install Apache
		$ sudo apt-get install apache2

	#**1.2 Configure Name-based Virtual Hosts
		$ sudo a2dissite *default
		$ cd /var/www
		create folder for frog
		$ sudo mkdir frog.com
		create folders to sotre websites'files, logs and backups
		$ sudo mkdir -p frog.com/public_html
		$ sudo mkdir -p frog.com/log
		$ sudo mkdir -p frog.com/backups
		create virtual host file
		$ sudo vim /etc/apache2/sites-available/frog.com.conf
		copy from configure/frog.com.conf

		Enable Frog website
		$ sudo a2ensite frog.com.conf
		Restart Apache
		$ sudo service apache2 restart

	#**1.3 Install MySQL
		$ sudo apt-get install mysql-server
		create Database for frog
		$ mysql -u root -p
		mysql> create database login;
		mysql> grant all on login.* to 'www-data';
		mysql> quit;
		initialize Database for frog
		mysql -u root -p < server/initialze.sql

	#**1.4 Install PHP
		$sudo apt-get install php5 php-pear
		$sudo apt-get install php5-mysql
		$sudo mkdir -p /var/log/php
		$sudo chown www-data /var/log/php
		$sudo service apache2 restart

# Step2: Set permission for frog
	$ sudo cd /var/www
	change owner of frog source code to yourself
	$ sudo chown -R your_username frog.com
	change group of frog soure code to Apache
	$ sudo chgrp -R www-data frog.com
	change permission to make frog executable by Apache
	$ sudo chmod -R 770 frog.com

# Step3: KLEE Configuration
	#**3.1 Add llvm-gcc to Apache path
	$ sudo vim /etc/apache/envvars
	Add the following lines to file:

		export C_INCLUDE_PATH=/usr/include/x86_64-linux-gnu
		export CPLUS_INCLUDE_PATH=/usr/include/x86_64-linux-gnu
		export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/var/www/frog.com/llvm-gcc4.2-2.9-x86_64-linux/bin"
	#**3.2 Add KLEE Dependency
	$sudo apt-get install g++ curl dejagnu subversion bison flex bc libcap-dev

# Step4: Install FROG tools
	$ sudo apt-get install astyle
