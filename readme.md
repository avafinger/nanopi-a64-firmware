NanoPi A64 Ubuntu Xenial Xerus 16.04 LXDE OS Image (firmware)
=============================================================

**Update:** Kernel version 3.10.105 with Blue Led (heartbeat)
**Update 2:** Camera with OV5640 activated and working


LXDE (Lightweight X11 Desktop Environment) is a desktop environment which is lightweight 
and fast and uses less RAM and less CPU while being a feature rich desktop environment.

If you want a richer desktop environment (but slower) you can install 
Ubuntu MATE on top of this Image and later de-install LXDE.

I use LXDE just because it is very fast, snappy  and responsive!
You can always improve, tweak and tune the way you want at any time.
This is a very LEAN and MEAN OS image to play and learn how to extend it.

We will flash the OS image in a very unusual way and do it manually.
Read **instructions section** on how to flash the image.


** THIS IS a WiP **

Disclaimer: Use at own risk

This is a LXDE OS image for the NanoPi A64
------------------------------------------

## Tested on NanoPi A64 board

- Camera (OV5640) - status: working
- Wifi (rtl8189es) - status: working
- HDMI 720P - status: working (a64-2GB.dtb_720P)
- HDMI 1080P - status: working (a64-2GB.dtb)
- GbE (Gigabit Ethernet) - status: working
- Kernel 3.10.104 - status: working
- Kernel 3.10.105 - status: working
- Leds (Blue) - status: working - "heartbeat"
- Firefox 64bit - stable


## Currently not working

- shutdown not always works, reboot most of the times

## NanoPi A64 Booting linux

[![NanoPI A64 Booting sequence](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/0.jpg)](https://youtu.be/0j9BPUnExdA)


Screenshots
-----------

Camera (OV5640)
![ov5640](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/camera.jpg)

1080P
![1080p60](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/1080p.png)

Wifi
![bluetooth](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/wifi.png)

Firefox
![bluetooth](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/firefox.png)

htop
![bluetooth](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/htop.png)

RTL8189ETV (8189es)
![bluetooth](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/rtl8189es.png)

Issues
------

- Shutdown


	If you shutdown (sudo shutdown -h or the Shutdown Button), most of the times (90%)
	the board will reboot, if you need to turn off the board click on Shutdown Button
	and wait for both leds turn off and then unplug the power cord, if you cut the power
	while the board is booting again you will corrupt the SD CARD!



- Board does not boot (what to do?)


	In rare occasions the board does not boot despite Blue Led is on heartbeating or
	it enters in a boot cycle (keep rebooting), it is usually safe to unplug 
	the power cord but always check card integrity after that.
 
    

	Try again to boot several times, sometimes it enters in the u-boot prompt.

   
  
	Change SD CARD and repeat the process.

     

	Find another USB Reader and repeat all over again with this USB Reader



Credits
-------

- Thanks to Yuefei (FriendlyArm) for the board
- FriendlyArm: http://www.friendlyarm.com/index.php?route=product/product&path=69&product_id=159
- Longsleep's kernel: https://github.com/longsleep/linux-pine64
- Armbian: https://www.armbian.com/
- @lex


Instructions
------------

Requirements:

	- We need a linux box
	
	- Install md5sum
	
	- PSU with at least 2.5A
	
	- Good SD CARD, 8GB minimum (find a good and trusted brand)
	
	- Good USB card reader (make sure you have a trusted USB card reader)


Assuming we have an USB card reader and our device is /dev/sdX where X is a letter [b,c..]
and in our example (change to your letter) my device is 'c', /dev/sdc.

Clone our nanopi-a64-firmware


	git clone https://github.com/avafinger/nanopi-a64-firmware

	cd nanopi-a64-firmware/



Rebuild our rootfs


	cat rootfs_nanopia64_rc1.tar.gz.0* > rootfs_nanopia64_rc1.tar.gz



Check if we have it correctly


	md5sum rootfs_nanopia64_rc1.tar.gz

	060b4d6f41fed693d578ab1bf94cd818  rootfs_nanopia64_rc1.tar.gz
	


Format the SD CARD and Flash (Warning: run as sudo or root and make sure you get the correct DEVICE letter)


	sudo chmod +x *.sh

	sudo ./format_sd.sh /dev/sdc

	sudo ./flash_sd.sh /dev/sdc



Now we have our SD CARD with the OS Image, boot with this card and Enjoy!


	user: ubuntu

	pasw: ubuntu


Camera (OV5640)

	To work with CAM500B (ov5640) and guvcview override
	a64-2GB.dtb with a64-2GB.dtb_OV5640


		mv /media/ubuntu/a64/a64-2GB.dtb /media/ubuntu/a64/a64-2GB.dtb_OK
		cp -af a64-2GB.dtb_OV5640 /media/ubuntu/a64/a64-2GB.dtb

	
History Log:
===========
* initial commit (readme file)
* kernel 3.10.104 RC3 (tested and working)
* screen images (WIP)
* Initial instructions (WIP)
* Camera (ov5640)
