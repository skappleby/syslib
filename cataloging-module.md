# Create a Bare Bones Cataloging Module, Part 2!

_Assignment Week 9_

*Reminder: syntax and directory location are important*

This week placed more emphasis on the way different pages interact with each other.
We made a basic html form so we could enter data
into our SQL database from a more user-friendly
interface, then created another php script file that 
actually will add the data we enter in the form into the database.

We also added an authentication file to the /etc/apache2 directory,
which is where the configuration files live. 

We set the username (where user is libcat)
and say that we're going to set a password 
```
sudo htpasswd -c /etc/apache2/.htpasswd libcat
```

Then we edit the config file in nano
```
sudo nano /etc/apache2/apache2.conf
```
And edit the stanza below so that *AllowOverride None*
reads *AllowOverride All*
```
<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride All
  Require all granted
</Directory>
```

And follow the other steps in [Dr. Burns' text](https://cseanburns.net/WWW/systems-librarianship/16.8-basic-opac-admin.html).
---

I'm really starting to get a sense of the way 
these systems work
at a very rudimentary level,
and that feels really cool.

