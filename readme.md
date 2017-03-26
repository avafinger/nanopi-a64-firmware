NanoPi A64 Ubuntu Xenial Xerus 16.04 LXDE OS Image (firmware)
=============================================================

**Update:** Kernel version 3.10.105 with Blue Led (heartbeat or SD Card activities)


LXDE (Lightweight X11 Desktop Environment) is a desktop environment which is lightweight 
and fast and uses less RAM and less CPU while being a feature rich desktop environment.

If you want a richer desktop environment (but slower) you can install 
Ubuntu MATE on top of this Image and later de-install LXDE.

I use LXDE just because it is very fast, snappy  and responsive!
You can always improve, tweak and tune the way you want at any time.
This is a very LEAN and MEAN OS image to play and learn how to extend it.

Disclaimer: Use at own risk

This is a LXDE OS image for the NanoPi A64
------------------------------------------

## Tested on NanoPi A64 board

- Wifi (rtl8189es) - status: working
- HDMI 720P - status: no 1080P only 720P
- GbE (Gigabit Ethernet) - status: working
- Kernel 3.10.104 - status: working


## Currently working

- Firefox 64bit - stable


## Currently not working

- OV5640 (camera) - status: not working, may need a revision
- HDMI 1080P - status: unable to set 1080P, may need a revision
- shutdown not always works, reboot most of the times

Screenshots
-----------

Wifi
![bluetooth](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/wifi.png)

Firefox
![bluetooth](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/firefox.png)

htop
![bluetooth](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/htop.png)

RTL8189ETV (8189es)
![bluetooth](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/rtl8189es.png)


Credits
-------

- FriendlyArm: http://www.friendlyarm.com/index.php?route=product/product&path=69&product_id=159
- Longsleep's kernel: https://github.com/longsleep/linux-pine64
- Armbian: https://www.armbian.com/
- @lex

History Log:
===========
* initial commit (readme file)
* kernel 3.10.104 RC3 (tested and working)
* screen images (WIP)
* Initial instructions (WIP)
