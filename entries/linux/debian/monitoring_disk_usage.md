I like to use the `wajig` tool for this.

One easy way to show how much space every installed package uses:
`wajig sizes` or for only the biggest packages `wajig large`.

Note: It is my understanding that the size here is a forehand approximation taken from the package meta-information in package management.

In my experience, this number is accurate. However it does not take into consideration the local data in `/var/`.

To get the total for all installed packages (in K):

```
wajig sizes |sed -E 's/^\S+\s+(\S+).+/\1/' | sed -E s/,// | awk '{s+=$1} END {print s}'
```

On the other hand, a `baobab` is a nice GUI tool to give you a top-down view of space usage by directory.

Sort of like `du -d 1 -h`, only fancier.

For a quick overview per partition nothing bets: `df -h`

In my experience you will find your *roughly* adding up in this way:  
```
Installed packages total + user data (/home/) + local data (/var/) = total space use
```
