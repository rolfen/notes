If you are running a command inside a Linux terminal (over SSH or otherwise), this command will normally be killed when you close the terminal session.

There is a way to have it survive the terminal and to come back to it later, *even if the command is already running*.

You'll need the `screen` and `reptyr` packages installed.

For the sake of example, let's have `htop` running.

```
$ htop
```

In a new terminal, find the PID of `htop`

```
$ ps aux|grep htop
john        9630  4.4  0.1   9356  5452 tty2     S+   22:03   0:56 htop
john        9683  0.0  0.0   6332  2024 pts/0    S+   22:24   0:00 grep htop
```

then start a `screen` session

```
$ screen
```

Inside the screen session, "bring over" `htop` by it's PID

```
$ reptyr 9630
```

Now it should be running right in front of us, in the screen session. On the old terminal (tty2) it should have stopped running with a message at the bottom

```
1+  [Stopped]     htop
```

The new terminal which hosts the screen session can safely be killed. `htop` will keep running inside the disconnected screen session which acts as a virtual terminal.

To go back to it, find the detached screen session:

```
$ screen -ls
There is a screen on:
        9690.pts-0.debian       (09/29/2023 10:27:59 PM)        (Detached)
1 Socket in /run/screen/S-rolf.
```

and reattach it:

```
$ screen -r 9690.pts-0.debian
```
