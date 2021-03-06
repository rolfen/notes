
These are some of the tasks that I typically do at some point after installing a new Debian system.

### Add myself to sudoers

This is generic Linux stuff.

```
su -
usermod -aG sudo myusername
```
Need to log off to apply changes.

### Add access to experimental packages
```
su -
# note: highest priority on top
echo 'deb http://deb.debian.org/debian experimental main' >> /etc/apt/sources.list
echo 'deb http://deb.debian.org/debian unstable main' >> /etc/apt/sources.list
# Get stable packages by default
echo 'APT::Default-Release "stable";' > /etc/apt/apt.conf.d/99defaultrelease
```

Also might be interesting to add access to `non-free` packages if it's not already there.

### Add `~/.local/bin` to PATH

For some reason, Debian does not add this directory to path by default, but `pip` installs binaries here by default.

Append the following to ~/.bashrc

```
# Debian missed this - pip-installed binaries go here
if [ -d "$HOME/.local/bin" ] ; then
    PATH="$HOME/.local/bin:$PATH"
fi
```



### Install a few useful packages

#### ... Package managment

 - `apt-file` can find the package provides a particular (usually executable) file  
 - `apt-listbugs` list any serious bug before installing a package. Useful for packages from `unstable` or `testing`

#### ... Terminal

`bash-completion` Autocompletion helper for command arguments whenever available

 Then possibly add autocomplete for commonly pinged domains  
 `complete -W 'two.eebe.be google.com' ping`

#### ... System monitoring

`htop` Alternative to `top`

### Configure `xfce4-terminal`

 - Open Edit -> Preferences
 - In the first tab "General", under label "Command", enable "Run command as login shell"
 
This will ensure that all the good stuff under `/etc/profile.d` (such as bash autocomplete) gets loaded.



