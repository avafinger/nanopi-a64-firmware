NanoPi A64 Ubuntu Xenial Xerus 16.04 LXDE OS Image (firmware)
=============================================================

**Update:** Kernel version 3.10.105 with Blue Led (heartbeat)

**Update 2:** Camera with OV5640 activated and working

**Update 3:** HW decode instructions: https://github.com/avafinger/cedrusH264_vdpau_A64

**Update 4:** New Image with some fixes and goodies: [see here](#install-new-image-with-some-fixesimprovement)

**Update 5:** fix for USB EHCI and OHCI plus Jack sound

**Update 6:** Firmware Image with support for PPP and GSM modems: [here](#instructions-for-firmware-image)

**Uodate 7:** Kodi on NanoPi A64 (2019): https://github.com/avafinger/nanopi-a64-firmware#kodi-on-nanopi-a64


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

## Install new Image with some fixes/improvement

- Compiled with **gcc 7.1**
- Blue Led is now fixed, is wired active low.
  added: led1_active_low = <0x1>;
- No more FAT, we are now able to update/upgrade kernel with linux-image deb package
- PPoE support enabled
- Built in analog sound (Jack)
- Faster boot time
- ssh is installed (v2)
- PPP and 3G/GSM modem support (Experimental)

Instructions for the new Image: [here](#instructions-for-new-image)

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
- HW decoding H264 (1080P)  - https://github.com/avafinger/cedrusH264_vdpau_A64
- USB highspeed and lowspeed - status: working

## Currently not working

- shutdown not always works, reboot most of the times

## NanoPi A64 Booting linux

[![NanoPI A64 Booting sequence](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/0.jpg)](https://youtu.be/0j9BPUnExdA)


## Camera (OV5640)
[![NanoPI A64 Booting sequence](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/camera.jpg)](https://youtu.be/UCD8cfAEmRE)


## HW decoding (1920x1080 H264) with cedrus
[![NanoPI A64 Cedrus](https://github.com/avafinger/nanopi-a64-firmware/raw/master/img/1920x1080.jpg)](https://youtu.be/mXMOh9ShDDc)


Screenshots
-----------

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

	
	HDMI 1080P and GbE draws a lot of power, check you PSU.
	

   
- Board never boots (what to do?)
  
		- Change SD CARD and repeat the process.
     
		- Find another USB Reader and repeat all over again with this USB Reader

		- The default setup is HDMI 1080P, try to switch to 720P,
		  use: https://github.com/avafinger/nanopi-a64-firmware/blob/master/a64-2GB.dtb_720P

- SPI

        Spi needs some attention, still need to work out the DT for spi device.



- BUG: soft lockup - CPU#0 stuck for 21s! 

	Latest kernel has this latent bug that can manifest or no in your board.
	This is related to a race condition and it predates Kernel 3.10.104 and afterwards
	so if you are afected by this bug try to unplug power cable, wait a few seconds and try again.
	I found this is probably due to the Wifi high load on trying to connect to the AP and can trigger
	the issue. Try to remove wpa_supplicant and wlan in /etc/network/interfaces if you can, maybe this can help

interesting reading can be found here and there:

	https://www.suse.com/support/kb/doc/?id=7017652

	https://github.com/longsleep/build-pine64-image/issues/51

	https://github.com/openhab/openhabian/issues/215



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

Find your SD CARD device after insert the SD CARD type:

        dmesg|tail


If you have a USB card reader the format would be some thing like this

        dmesg|tail
        [97286.659006] sdc: detected capacity change from 15523119104 to 0
        [99023.137526] sd 4:0:0:0: [sdc] 30318592 512-byte logical blocks: (15.5 GB/14.4 GiB)
        [99023.147516] sd 4:0:0:0: [sdc] No Caching mode page found
        [99023.147521] sd 4:0:0:0: [sdc] Assuming drive cache: write through
        [99023.162514] sd 4:0:0:0: [sdc] No Caching mode page found
        [99023.162518] sd 4:0:0:0: [sdc] Assuming drive cache: write through
        [99023.168535]  sdc: sdc1 sdc2

Type:

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


Add the camera modules to /etc/modules


	dw9714_act
	ov5640
	vfe_v4l2


Instructions for new Image
--------------------------

- Build v1 (works only the lower USB receptacule with high speed hub)

Rebuild our new kernel:


        cat rootfs_nanopia64_rc2.tar.gz.0* > rootfs_nanopia64_rc2.tar.gz


Check MD5 (must match with this):

        md5sum boot_nanopia64_rc2.tar.gz
        154350af7abdcf1062130c0b68bc1071  boot_nanopia64_rc2.tar.gz

and

        md5sum rootfs_nanopia64_rc2.tar.gz
        81be98d5f36ec6d42178028c0ab05fce  rootfs_nanopia64_rc2.tar.gz


- **Build v2** (works all USB receptacules)

Rebuild our new kernel:


        cat rootfs_nanopia64_rc3.tar.gz.0* > rootfs_nanopia64_rc3.tar.gz


Check MD5 (must match with this):

        md5sum boot_nanopia64_rc3.tar.gz
        e4d1ff4ba4740900ecaf65bd357b022b  boot_nanopia64_rc3.tar.gz

and

        md5sum rootfs_nanopia64_rc3.tar.gz
        ad78376f488e417e05e780007c2538e0  rootfs_nanopia64_rc3.tar.gz


Find your SD CARD device after insert the SD CARD type:

        dmesg|tail


If you have a USB card reader the format would be some thing like this

        dmesg|tail
        [97286.659006] sdc: detected capacity change from 15523119104 to 0
        [99023.137526] sd 4:0:0:0: [sdc] 30318592 512-byte logical blocks: (15.5 GB/14.4 GiB)
        [99023.147516] sd 4:0:0:0: [sdc] No Caching mode page found
        [99023.147521] sd 4:0:0:0: [sdc] Assuming drive cache: write through
        [99023.162514] sd 4:0:0:0: [sdc] No Caching mode page found
        [99023.162518] sd 4:0:0:0: [sdc] Assuming drive cache: write through
        [99023.168535]  sdc: sdc1 sdc2

If you have a SD CARD reader embedded in your laptop, the format would be like this:


        dmesg|tail
        [63376.329036] mmc0: new SDHC card at address 1234
        [63376.368234] mmcblk0: mmc0:1234 SA04G 3.67 GiB 
        [63376.368372]  mmcblk0: p1 p2


Flash New Image to SD CARD, type in shell:


        sudo chmod +x *.sh


- Build v1

        sudo ./burn_sdcard.sh /dev/sdc

or

        sudo ./burn_sdcard.sh /dev/mmcblk0


- **Build v2**

        sudo ./burn_sdcard_v2.sh /dev/sdc

or

        sudo ./burn_sdcard_v2.sh /dev/mmcblk0


wait untill finish. Remove the SD CARD and boot you device with the SD CARD inserted and Enjoy!


## Instructions for Firmware Image

There is an experimental Firmware Image to be flashed onto 8 GB sd card (or greater) using your preferred Disk Utility.
It is highly recomended to use a good SD card and a good SDHC card Reader and Writer. Use a trusted brand.

- Download from here
	
	https://mega.nz/#F!9OxRnCya!6fsKg-X0tp76Pw89RdMspw

It has been Zipped to save space with **7zip**, please unzip before burning.
Use **Win32DiskImager** or a good disk imager.

## Kodi on NanoPi A64

There is a pre-release image with mainline kernel 4.20.17 with Kodi 18.3 RC1.
If you would to test and see if works for you.
Go to: https://github.com/avafinger/nanopi-a64-kodi


History Log:
===========
* initial commit (readme file)
* kernel 3.10.104 RC3 (tested and working)
* screen images (WIP)
* Initial instructions (WIP)
* Camera (ov5640)
* HW Decoding H264 (https://github.com/avafinger/cedrusH264_vdpau_A64)
* New OS Image
* USB fix (ECHI and OHCI works on all USB connectors)
* PPP and 3G/GSM modem support
* latent BUG: **soft lockup - CPU#0 stuck for 21s!** 
* Kodi on A64 (pre-release
