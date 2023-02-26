# LAMP Setup

**Notes on installing and configuing Apache, PHP, and MySQL on a Linux server**

(LAMP = Linux, Apache, MySQL, PHP)

_Assignment Week 7_

## Step 1: Apache

1. Gotta update
```
sudo apt upgrade
```
Press y

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
