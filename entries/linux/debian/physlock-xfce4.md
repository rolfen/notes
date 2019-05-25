physlock is a minimal (text) screen locker that also locks all terminals.

First uninstall any present screen locker such as light-locker

After installing physlock (apt-get), you will have to configure it to run when you suspend or hibernate. Add the following service definition:

```
sudo nano /etc/systemd/system/physlock.service
```

```
[Unit]
Description=Lock when asleep
Before=sleep.target hibernate.target hybrid-sleep.target

[Service]
Type=forking
ExecStart=/usr/bin/physlock -d

[Install]
WantedBy=sleep.target hibernate.target hybrid-sleep.target
```

`physlock -d` and `Type=forking` will make sure that physlock is running *before* the computer goes to sleep, so that there is no delay in displaying the lock screen when it wakes up.


Update services configuration and enable physock:

```
sudo systemctl daemon-reload
sudo systemctl enable physlock.service
```

## Integration with xfce4

To have the xfce4 "Lock screen" buttons and keyboard shortcuts trigger `physlock`, we need to modify the `/usr/bin/xflock4` script

Just look for the list of screen-locking commands that the script tries, and add `physlock` at the end, as such:

```
for lock_cmd in \
    "xscreensaver-command -lock" \
    "light-locker-command --lock" \
    "gnome-screensaver-command --lock" \
    "mate-screensaver-command --lock" 
do
```

Becomes: 

```
for lock_cmd in \
    "xscreensaver-command -lock" \
    "light-locker-command --lock" \
    "gnome-screensaver-command --lock" \
    "mate-screensaver-command --lock" \
    "physlock"
do
```
