# Omeka Install

Notes on the info and processes from this week, the week when I have to try to figure it out on my own.

_Assignment Week 11_

### Create a new user and database

Starting out by creating a new user and new database in MySQL for Omeka,
using the same instructions from the 
[WordPress install](https://cseanburns.net/WWW/systems-librarianship/17-install-wordpress.html)
handbook instructions, so...
```
sudo su
mysql -u root
```
...to get into the MySQL command prompt and
change to the root user. _Remember to be careful
as root!_

In the MySQL command prompt, I modified the commands
from the WordPress install and did this:
```
create user 'omeka'@'localhost' identified by 'XXXXXXXXX';
create database omeka;
grant all privileges on omeka.* to 'omeka'@'localhost';
show databases;
```
I was incredibly relieved to see my omeka database in the list
and I only forgot the `;` to end the command one time!

So then I `\q` to quit MySQL
and `exit` to quit being root user
because it makes me nervous.

---

### Download and extract

Switched to **/var/www/html** for the next bit of business
and ran the following to download Omeka Classic:
```
sudo wget https://github.com/omeka/Omeka/releases/download/v3.1/omeka-3.1.zip
```
Then I looked at the directions again and realized I needed
to install the `unzip` command to open it, which I probably should've
done first, but I ran
```
sudo apt install unzip
sudo unzip omeka-3.1
```
and a bunch of stuff happened so I think I was successful!

I did decide to change the directory name to just **omeka**,
which I did with the command:
```
sudo mv omeka-3.1 omeka
```

---

### Add credentials and change file ownership

Starting by saying that I probably should have copied
**db.ini** before making the config modifications,
but I didn't, so we're moving on.

What I did do was:
```
cd omeka
sudo nano db.ini
```
and entered my credentials that I created
in the first steps in the **XXXXXX** values fields.

Since I only need to change file ownership
on the `files` directory, I ran the following
(reminder that I'm still in **/var/www/html/omeka**
when I do this):
```
cd files
sudo chown -R www-data:www-data *
sudo systemctl restart apache2
sudo systemctl restart mysql
```
The documentation directed me to restart Apache2 and MySQL,
which explains the last 2 commands.

---

## Omeka is here!

Access and activate the Omeka instance by
going to **http://my-ip-address/omeka** and 
completing the web form. It's working!
