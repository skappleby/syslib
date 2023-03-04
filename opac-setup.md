# Creating a Bare Bones OPAC

Notes on the info and processes from this week

_Assignment Week 8_

**Make sure you're in the right directory**

I started by writing the files in my home directory and then the php script couldn't find them. Once I was working in `/var/www/html` where all the other opac-related files were, I was in business.
Also important to remember when pushing/pulling to Github to be in `/repos/syslib`!

Related to this, pay attention to syntax! Small errors like forgetting punctuation in a MySQL command or pointing to the wrong file (or typing the wrong file extension) sucks.

When everything works, you're really just telling the computer where to go to look for stuff and how you want it displayed to the user.

---
It's kind of fascinating to see how a database search interface works in an
extremely simplified way.
Obviously, a real OPAC is going to be
much more elabotate with many tens of thousands
(millions?) of complex entries and fields and tables,
but having the opportunity to see a very simple php script
and getting a chance to read it line by line
and deduce that this command is retrieving that object
really helps put the search action into perspective.
