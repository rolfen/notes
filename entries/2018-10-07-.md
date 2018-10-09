---
published: false
---
## The blog thing

Today, I start this blog thing.

The core idea is to document tech work so that:
- It can serve as a reference later on
- It can help others with similar difficulties
- Bring credit and recognition to my skills

I have privacy concerns - to keep things simple, I might just put all the personal and other non-tech stuff in another blog.

The content is hosted on github. It can be edited online through stackedit.io or prose.io. I prefer prose.io. stackedit.io seems to leave some unwanted metadata at the bottom of the file. 

I have yet to see how I will be publishing it. Maybe Jeckyll.


## LDAP on Debian

After setting up a mail server using [Thomas Leister's great article](https://thomas-leister.de/en/mailserver-debian-stretch/), I started looking into LDAP, mainly for storing user passwords.

Yesterday, I managed to set up a rudimentary LDAP service (slapd).

As a next step, I'm looking into LDAP clients to experiment with it.

I installed phpldapadmin and am in the process of configuring /etc/phpldapadmin/config.php 

First, the obvious; I replace all instances of (dc=example,dc=com) with my domain. Then I enable long through `bind_id`. I'm following [these instructions](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-openldap-and-phpldapadmin-on-ubuntu-16-04) (despite being on Debian 9.5 (stretch)).

I also reoved the annoying template warnings (hide_template_warning).

I create a pretty standard nginx virtual host, and add SSL certificate using certbot.

Todo:
 - Check LDAP Security - I think we have to disable "simple authentication"
 - Do something useful with it (such as pam_ldap)
 - Test
