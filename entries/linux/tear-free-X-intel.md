There is a config option to stop screen tearing.

This is how I checked that I am running an Intel GPU
```
lsmod |grep i915
```

On my system, I added this config file:
```
sudo nano /usr/share/X11/xorg.conf.d/20.intel.conf
```


With contents:
```
Section "Device"
    Identifier "Intel Graphics"
    Driver "intel" 
    Option "TearFree" "true"
EndSection
```
