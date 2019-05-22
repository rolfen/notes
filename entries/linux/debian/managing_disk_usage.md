## Detecting big packages

I like to use the `wajig` tool for this.

One easy way to show how much space every installed package uses:
`wajig sizes` or for only the biggest packages `wajig large`.

Note: It is my understanding that the sizes given here are taken from the package meta-information. In other words, this is how much space theis package should be using, according to the package maintainer.

In my experience, this number is accurate. However it does not take into consideration any related data in `/var/`.

To get the total for all installed packages (in K):

```
wajig sizes |sed -E 's/^\S+\s+(\S+).+/\1/' | sed -E s/,// | awk '{s+=$1} END {print s}'
```

## Detecting big directories / files

On the other hand, the `baobab` is a nice GUI tool to give you a top-down view of space usage by directory.

Sort of like `du -d 1 -h`, only fancier.

For a quick overview per partition nothing beats: `df -h`

In my experience you will find your numbers *roughly* adding up in this way:  
```
Installed packages total + user data (/home/) + local data (/var/) = total space use
```

## Detecting unused packages

`deborphan` and then `orphan` to remove them.


## Preventing leftovers

Package managers are a good way to install and uninstall applications in a neat way.

However, sometimes you would want to build from source.

In these cases, it is recommended to use the `equivs-build` tool for quickly creating virtual package which keep track of build dependencies for a particular project.

http://www.linuxcertif.com/man/1/equivs-build/

https://www.unixdaemon.net/linux/creating-debian-virtual-packages/
