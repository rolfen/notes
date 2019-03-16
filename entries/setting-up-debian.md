
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
# we don't want all our system to be updated from experimental
echo 'APT::Default-Release "stable";' > /etc/apt/apt.conf.d/99defaultrelease
```

### Add `~/.local/bin` to PATH

For some reason, Debian does not add this directory to path by default, but `pip` installs binaries here by default.

Append the following to ~/.profile

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

#### ... System monitoring

`htop` Alternative to `top`
