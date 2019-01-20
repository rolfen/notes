
These are some of the tasks that I typically do at some point after installing a new Debian system.

### Add myself to sudoers
```
su -
usermod -aG sudo myusername
```
Need to log off to apply changes.

### Adding access to experimental packages
```
su -
# note: highest priority on top
echo 'deb http://deb.debian.org/debian experimental main' >> /etc/apt/sources.list
echo 'deb http://deb.debian.org/debian unstable main' >> /etc/apt/sources.list
# we don't want all our system to be updated from experimental
echo 'APT::Default-Release "stable";' > /etc/apt/apt.conf.d/99defaultrelease
```

### Some useful tools

#### apt-file

`apt-file` can find the package provides a particular (usually executable) file:  
`apt-get install apt-file`
