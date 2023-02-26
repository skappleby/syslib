
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
		- `sudo nano info.php` to create the info.php file
		- text for php file:
```
<?php
phpinfo();
?>
```
		- open file using  external IP address to view the system information: **http://IP-ADDRESS/info.php**

