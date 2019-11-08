Linux can be really cool and this is one of these times.

```
sudo apt-get install sshfs 
sudo mkdir /mnt/tecmint
chmod 777 /mnt/tecmint
sshfs tecmint@x.x.x.x:/home/tecmint/ /mnt/tecmint
sudo sshfs -o allow_other tecmint@x.x.x.x:/home/tecmint/ /mnt/tecmint
```

If all goes well you will have a mountpoint under /mnt/tecmint.

[Source](https://www.tecmint.com/sshfs-mount-remote-linux-filesystem-directory-using-ssh/)
