# WordPress Install

Notes on the info and processes from this week

_Assignment Week 10_

I'm installing WP from the [WordPress.org](https://wordpress.org/) site, 
so I need to check that my versions of PHP and MySQL
are compatible and up to date.

I ran `sudo apt update` when getting started to check for all 
system updates and performed the recommended updates by running 
`sudo apt upgrade`. Then I checked my system versions with:
```
php --version
mysql --version
```
I'm compliant! I'm running PHP v.7.4.3 and MySQL v.8.0

Installing WP from scratch from [Dr. Burns' directions](https://cseanburns.net/WWW/systems-librarianship/17-install-wordpress.html)
progressed easily.

The piece that I initially missed during the install
was the script to **change file ownership**. 
It was this important little bit:
```
sudo chown -R www-data:www-data *
```
I ran that from my base directory, `/var/www/html/wordpress`,
and that allowed me to add images and install additional
themes to my WP instance. Without that command, I kept getting
errors that said the system couldn't create a new directory.
Important stuff! 

---

Command line work is really not so intimidating.
I still feel a little like I'm just tracing the lines
that someone else drew, but maybe that's how I learn this?
I do feel like I'm understanding more and it's exciting
to not be so anxious about what I'm doing.

I'm also just a tiny bit proud of the wordpress site
for the [Troy McClure Memorial Library](http://34.85.146.164/wordpress/).
