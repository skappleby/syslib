## Installing a new VM using PuTTY (again)

[This YouTube video is super helpful](https://www.youtube.com/watch?v=fmh94mNQHQc)
and the source for all of this.

Open PuTTYgen and click **Generate**
then move the mouse around per the directions
to generate a key pair.

**Key comment:** is actually the user name
we'll use to connect to the VM, so change 
it to something that makes sense in this context.

Click **Save private key** and save
without a passphrase.

Copy the public key text and add it
to the VM instance:
- go to VM instance details and click **Edit**
- paste public key in the **Security and Access** section
- save changes

From the dashboard, copy the 
external IP for the VM and
paste in the **Host Name (or IP address)** field.

Go to **SSH** in the side nav menu
and click to expand. Then click **Auth**
and **Credentials**. Browse to the private key 
file associated with the VM and double-click
to add.

Click **Open** and login as the user.

---

I had to go through these steps 
when I created a new virtual machine to 
do the Koha install, so I figured it was best
to document it this time so I don't
forget whenever I have to do it again.

Once I sorted this out, the Koha install
went just fine. It was just a matter of reading
[Dr. Burns' directions](https://cseanburns.net/WWW/systems-librarianship/20-install-koha.html)
and following the [Koha documentation](https://koha-community.org/manual//22.11/en/html/index.html).
