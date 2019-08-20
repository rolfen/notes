Disable the annoying **BEEP**.

```
echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf
```

Temporarily:
```
rmmod pcspkr
```
