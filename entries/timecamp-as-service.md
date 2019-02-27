The timecamp client for Linux installs itself by default, as an autorun desktop application.
You can see it in Gnome Tweaks, under "Startup Applications".

The issue with this setup is that it will not restart itself in case of failure, so you can silently lose days worth of logging if timecamp crashes, which happened to me.

My solution is to install this as user service instead.

First, you should have run the timecamp desktop app so that the setup would be completed.

Create a user service definition:

```
cd ~/.config/systemd/user
nano timecamp.service
```

Containing the following:

```
[Unit]
Description=Timecamp Spying Daemon

[Service]
Restart=always
ExecStart=/usr/share/timecamp/timecamp

[Install]
WantedBy=multi-user.target
```

The interesting part here is `Restart=always` under `[Service]`. It will ensure that the client is brought back up in case it dies.

Remove the timecamp autostart entry using Gnome Tweaks, and kill any running timecamp client:

```
pkill timecamp
```

Then start our shiny new service for the first time:

``` 
systemctl --user daemon-reload
systemctl --user enable timecamp.service
systemctl --user start timecamp.service
```
