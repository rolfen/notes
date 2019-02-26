## Investigating server bandwidth

I have noticed abnormal bandwidth usage on my server, for a while now. The servers hosts a couple of low-traffic and also serves as a mail server and a VPN. A while back I installed a few tools that I thought would help me monitor the traffic. Each tools gives me a bit of information, but it's still an unresolved puzzle.

`vnstat` is a command line tool. I like it, although it tells me that something is going on, but gives me no indication of the source. Here `tun0` is the VPN interface.

```
~$ vnstat

                      rx      /      tx      /     total    /   estimated
 tun0:
       Sep '18    307.57 MiB  /    4.19 GiB  /    4.49 GiB
       Oct '18     31.85 MiB  /  543.88 MiB  /  575.73 MiB  /    1.99 GiB
     yesterday      4.11 MiB  /   77.88 MiB  /   81.99 MiB
         today         0 KiB  /       1 KiB  /       1 KiB  /      --

 eth0:
       Sep '18     12.07 GiB  /   13.28 GiB  /   25.35 GiB
       Oct '18    962.27 MiB  /    1.29 GiB  /    2.23 GiB  /    7.95 GiB
     yesterday    127.61 MiB  /  179.10 MiB  /  306.71 MiB
         today     48.23 MiB  /   54.99 MiB  /  103.21 MiB  /     141 MiB
```


As you can see, 10GiB of inbound data in September does not sound right. I wonder if this includes portscans, brute force login attempts, etc.

So I do some research and learn that atop has a `netatop` modules and it can be made to record bandwidth usage for each process.

I follow [these installation instructions](https://www.reddit.com/r/debian/comments/991ov6/problem_installing_netatop/e4linhm). 

Specifically:

	$ sudo apt install linux-headers-$(uname -r) make zlib1g-dev
	$ wget https://www.atoptool.nl/download/netatop-2.0.tar.gz
	$ tar xvf netatop-2.0.tar.gz
	$ cd netatop-2.0
	$ make
	$ sudo make install
	$ sudo modprobe -v netatop
	$ sudo systemctl enable netatopd

However the last step fails:

	Failed to enable unit: File netatopd.service: No such file or directory
	
There is no `netatop` service.. However I can still launch it manually:

	sudo /usr/sbin/netatopd
	
So I create a very simple `netatopd.service` file in `/etc/systemd/system/` with the following contents:

```
[Unit]
Description=NetAtop Daemon

[Service]
Type=forking
ExecStart=/usr/sbin/netatopd

[Install]
WantedBy=multi-user.target
```

Now I can successfully enable it

	 sudo systemctl enable netatopd

Now I get networking statistics in `atop`! 

	sudo atop -n

At first I had tried 

	atop -n
	Kernel module 'netatop' not active; request ignored!
	
I did spend some time investigating this, before trying `sudo`. I didn't expect `atop` to need superuser privileges.

Anyway, watching the traffic, I periodically a simultaneous micro spikes in "unbound", "rspamd" and "redis" which seems to be related to email.

But really hardly any traffic unless I do something such as use webmail and send a big mail. So where did this traffic come from then?

To get a better idea of the relation between eth0 and tun0 traffic in vnstat, I run a test; I watch a youtube video on my phone through VPN whilst running `vnstat -l`

Here is what I get:

```
 tun0  /  traffic statistics
                           rx         |       tx
--------------------------------------+------------------
  bytes                     1.26 MiB  |       40.76 MiB

 eth0  /  traffic statistics
                           rx         |       tx
--------------------------------------+------------------
  bytes                    43.35 MiB  |       45.08 MiB
```
This capture lasted 9.2 minutes.

It makes sense: VPN traffic is counted on eth0 when it is received from youtube (rx), and then again when it is sent to the VPN client (tx).

