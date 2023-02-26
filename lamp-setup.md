
# LAMP Setup

**Notes on installing and configuing Apache, PHP, and MySQL on a Linux server**

(LAMP = Linux, Apache, MySQL, PHP)

_Assignment Week 7_

### Step 1: Apache

Before install, update system:
```
sudo apt upgrade
```
Press **y** when prompted

1. Install Apache2 using `apt`
	- use `sudo apt search apache2 | head`
		- piping `apt search` through `head` searches the top 10 lines of the searched files and limits the number of results to a manageable amount
	- `apt show apache2` to confirm this is the package we're looking for
	- install using `sudo apt install apache2`
		- press **y** when prompted to continue
1. Run basic checks
	- use `systemctl` to ensure apache2 is enabled and running
		- `systemctl list-unit-files apache2.service` command output shows apache2 is enabled
		- `systemctl status apache2` command output shows that apache2 is active
1. Install command line web browser and check default apache2 web page
	- `sudo apt install w3m` to install w3m as the browser
	- use loopback IP address to visit default site: `w3m localhost`
	- if it worked right, you should see **It works!** near the top of the screen
	- to exit `w3m`: **q** then **y**
	- we can also check in a regular web browser by using public IP address
		- find this on **Google Cloud Console > Compute Engine > VM instances** and click **External IP**
		- it's the same IP we use when we start PuTTY
		- if browser defaults to **https://** just make sure we type **http://**IP-ADDRESS to get it to work
1. Make a web page
	- navigate to the location of the document root of the default site: `cd /var/www/html/`
	- `ls` to see that there is an index.html file already; that's the apache2 default page
	- we renamed the original index file index.html.original and created a new one
		- to rename: `sudo mv index.html index.html.original`
		- to create the new index file: sudo nano index.html
		- add whatever html code in nano; for this exercise I copied and pasted the basic code from Dr. Burns' handbook
		-_note that we use `sudo` because we are outside the home directory, so be careful about running commands
	- reload the page or type external IP in the broswer URL to see the new page
		- to see the previous index page that we renamed, type **http://IP-ADDRESS/index.html.original**

### Step 2: PHP

1. Install PHP
	- use `apt install` to install PHP and modules: `sudo apt install php libapache2-mod-php`
		- running `apt show php` and `apt show libapache2-mod-php` gives more information about each package
	- restart apache 2: `sudo systemctl status restart apache2`
	- check status for errors: `systemctl status apache2`
2. Check install
	- create a small php file in the web document root to make sure it's installed properly
		- `cd /var/www/html/` to get to web document directory
		- `sudo nano info.php` to create the info.php file (see below for file text)
		- open file using  external IP address to view the system information: **http://IP-ADDRESS/info.php**
3. Modfy basic configurations
	- if we want apache2 to default to index.php instead of index.html, we need to configure that in the dir.conf file in **/etc/apache2/mods-enabled/**
	- navigate to /etc/apache2/mods-enabled/
	- create a backup of dir.conf before making modifications: `sudo cp dir.conf dir.conf.bak`
	- modify the dir.conf file: `sudo nano dir.conf` 
		- change the DirectoryIndex line to read: `DirectoryIndex index.php index.html index.pl index.xhtml index.htm`
		- we moved index.php ahead of index.html and deleted index.php in its old position, so apache2 will serve index.php by default first
	- use `apachectl configtest` to check configuration
		- should get **Syntax OK** message
	- reload: `sudo systemctl reload apache2`
	- restart: `sudo systemctl restart apache2`
4. Create index.php file
	- navigate back to apache2 document  root directory: `cd /var/www/html/`
	- create an index.php file: `sudo nano index.php` (see below for code text)
	- visit external IP address in browser to see index.php returned

_text for info.php file_
```
<?php
phpinfo();
?>
```

_text code for index.php file_
```
<html>
<head>
<title>Broswer Detector</title>
</head>
<body>
<p>You are using the following browser to view this site:</p>

<?php
echo $_SERVER['HTTP_USER_AGENT'] . "\n\n";

$browser = get_browser(null, true);
print_r($browser);
?>
</body>
</html>
```

### Step 4: MySQL

_A note to pay attention to the difference in prompts between MySQL and Linux. I'll use > to indicate a mysql command prompt. Check that syntax carefully in MySQL! Don't forget to end commands with `;`!_

1. Install and set up MySQL
	- locate and install: `sudo apt install mysql-server`
	- make sure it's running: `systemctl status mysql`
	- log in to the database to test as the root Linux user: `sudo su`
		- _be careful when doing anything as the root user lest you eff it all up!_
		- as root user, run `mysql -u root`
2. Create a regular user account (I created user1), set up practice database, grant user privileges
	- `> create user 'user1'@'localhost' identified by 'PASSWORD';`
		- should return Query OK message
	- create practice database called opacdb: `> create database opacdb;`
	- grant all privileges to user1: `grant all privileges on opacdb.* to 'user1'@'localhost';`
	- run `> show databases;` to make sure opacdb is there
	- exit MySQL as root user with `\q` then exit out of root Linux user with `exit`
3. Log in and make some tables
	- to log in: `mysql -u user1 -p` then enter password
		- the cursor won't move... don't be alarmed
	- refer to [Section 5.3 in Dr. Burns' handbook](https://cseanburns.net/WWW/systems-librarianship/16-installing-configuring-mysql.html) for examples of using **create, insert, alter, select, describe, delete**
	- use this data (or similar) to construct the table **and remember to pay attention to your syntax**
	- `> \q` to quit MySQL
1. Install PHP and MySQL support
	- install some modules to establish the connection between PHP and My SQL: `sudo apt install php-mysql php-mysqli`
	- restart apache2: `sudo systemctl restart apache2`
	- restart MySQL: `sudo systemctl restart mysql`
	- create a login.php file in /var/www/html so that PHP can authenticate when connecting to MySQL and change permissions so that the file can only be read by the apache2 server (see code below)
	- open login.php to add credentials: `sudo nano login.php` then enter credentials shown below.
	- create a new php file: `sudo nano opac.php`
		- copied the opac.php code from [Section 5.3, Create PHP Scripts](https://cseanburns.net/WWW/systems-librarianship/16-installing-configuring-mysql.html)
	- save and exit
1. Test!
```
sudo php -f login.php
sudo php -f index.php
```

Go back to external IP address in browser and add /opac.php to the URL. You should see the basic OPAC!

_Code to create login.php and modify permissions/ownership_
```
cd /var/www/html/
sudo touch login.php
sudo chmod 640 login.php
sudo chown :www-data login.php
ls -l login.php
```

_Content for login.php file_
```
<?php // login.php
$db_hostname = "localhost";
$db_database = "opacdb";
$db_username = "user1";
$db_password = "XXXXXXXXX";
?>
```

***I did it!***
