---
title: Samsung Tips-n-Tricks
author: PipisCrew
date: 2016-11-12
categories: [android]
toc: true
---

### ~~Restore STOCK ROM~~

1-restore STOCK ROM #through download mode# with ODIN v3.09 (PDA or AP option) (use home+volume down+power till logo appear)
	Go to #Original Recovery Mode#  (use home+volume up+power till logo appear)
	Perform Wipe Data/Factory Reset and Wipe Cache Partition
	reboot
2-find custom recovery for your device by http://teamw.in/Devices/ (warning download the .tar flavor) OR use clockwork-touch-6.0.4.1-n7105.tar
	power off
3-flash custom recovery with ODIN v3.09 (PDA or AP option) (use home+volume down+power till logo appear)
	boot to OS
	Jasin2169:after flashing recovery i recommend to launch recovery and then reboot because install-recovery.sh is replaced by stock recovery sometimes if ee dont reboot in custom recovery after flashing
4-copy to SDCard the UPDATE-SuperSU-v2.76-20160630161323, go to recovery and flash it!
	power off
5-goto TWRP #through custom recovery# (use home+volume up+power till logo appear)
	install > choose UPDATE-SuperSU-v2.76-20160630161323
	Wipe cache/dalvik
	Reboot
6-use Titanium to uninstall any app
--currently truly flight!! with STOCK ROM + ROOT only.

Safe to Remove List - [XLS](https://spreadsheets.google.com/spreadsheet/pub?hl=en_US&hl=en_US&key=0AnO2-4y6yE1gdDJRekl4QmkyNmIzUmRvX2h3UDVkQXc&output=html) - http://forum.xda-developers.com/showthread.php?t=1910885

* * *

### ~~Custom ROM~~

- copy the 08.15-wilson3q.zip + 08.17.opengapps-mini to sdcard (http://forum.xda-developers.com/galaxy-note-2/development-n7105/rom-unofficial-build-t3067695)
if (CWM)
	- boot on CWM recovery
	- Wipe data/Factory reset
	- Wipe Cache Partition
	- Mounts and Storage> Format / data
	- Advanced > Wipe Dalvik Cache > Yes
	- Mounts and Storage > Format System
if (TWRP)
	On main menu select > 'Wipe' > 'Swipe to Factory Reset' on the bottom of screen.
	Wipe > Advanced > Tick 'System' > Swipe

- Install Zip from sdcard > Choose zip from sdcard > 08.15-wilson3q.zip
- Install Zip from sdcard > Choose zip from sdcard > 08.17.opengapps-mini.zip

-reboot
- setup the device (g account, device config), when try to use titaniumbackup, informs me that there is no root access.

- poweroff
- boot on CWM recovery
- reflashSU (every time, I restored a ROM, root access disappear, have to power off and reflashSU)

* * *

### ~~Custom ROM - Clean Install~~

01-power off > put on download mode (use home+volume down+power till logo appear)
02-flash to N7105XXUEMK9_N7105XEFEMK1_XEF.zip via Odin
03-boot to *STOCK recovery* - perform Wipe Data/Factory Reset and Wipe Cache Partition
04-boot normally, stay for 10min on this OS (dummy, without g account)
05-power off > put on download mode (use home+volume down+power till logo appear)
06-download twrp-3.0.2-0-t0lte.img for G7105 - rename twrp-3.0.2-0-t0lte.img to recovery.img > open 7zip > compress the recovery.img to whatever.tar > flash through AP or PDA
07-device restarted - plug to USB - copy cm-12.1-20150914-UNOFFICIAL-wilson3q-t0lte.zip + open_gapps-arm-5.1-pico-20160828.zip to sdcard
08-reboot to *TWRP Recovery* (use home+volume up+power till logo appear) - perform :
a)On main menu select > ‘Wipe’ > ‘Swipe to Factory Reset’ on the bottom of screen.
b)On main menu select > ‘Wipe’ > 'Advanced' > Tick ‘System’ > Swipe on the bottom of screen.
09-flash cm-12.1-20150914-UNOFFICIAL-wilson3q-t0lte.zip + open_gapps-arm-5.1-pico-20160828.zip at once > then asked for 'Wipe Dalvik Cache' do it > Reboot > Ask to install SuperSU doit!

* * *

### ~~Latest TWRP for N7105~~

1-download latest @ https://dl.twrp.me/t0lte/
2-if is .img, you have to turn it to .tar (to be compatible with Odin)
3-rename *.img to recovery.img > open 7zip > compress the recovery.img to whatever.tar > flash through Odin > AP or PDA

http://www.xda-developers.com/how-to-install-twrp/
http://forum.xda-developers.com/note-4/general/convert-twrp-img-to-tar-odineasy-t3355944

* * *

### ~~GPS~~

Edit the /system/etc/gps.conf file.

You will need to find out which are closest to your region, you can find out here http://www.pool.ntp.org/zone/

//source - http://forum.xda-developers.com/showthread.php?t=939385
NTP_SERVER=europe.pool.ntp.org
XTRA_SERVER_1=0.europe.pool.ntp.org
XTRA_SERVER_2=1.europe.pool.ntp.org
XTRA_SERVER_3=2.europe.pool.ntp.org
XTRA_SERVER_4=3.europe.pool.ntp.org

SUPL_HOST=supl.google.com
SUPL_PORT=7276

or use https://play.google.com/store/apps/details?id=by.zatta.agps

* * *

### ~~Wifi Passwords~~

data\misc\wifi\wpa_supplicant.conf
That code only works if you are running a stock ROM.

* * *

### ~~Service Mode~~

to enter @ service mode dial : 
*#0011#
you have to do the trick :
menu > back
menu > input > uppercase > Q
menu > input > 0000
wait 20seconds, you get the menu go at :
UTMS > COMMON > NV REBUILD > writes "Not support in custom library"

-- or use phoneinfo -  https://play.google.com/store/apps/details?id=org.vndnguyen.phoneinfo

* * *

### ~~Backup SDCard~~

How to backup compressed data from your android device to your computer - http://forum.xda-developers.com/android/software-hacking/how-to-backup-compressed-data-android-t3464777
ADB sync utility - adbsync - http://forum.xda-developers.com/showthread.php?t=1898358 || http://forum.xda-developers.com/showthread.php?t=2133312 || https://github.com/google/adb-sync

* * *

Mokee ROM - http://download.mokeedev.com/?device=t0lte&type=release

Doing OTA updates ;) 

No reason to flash SuperSU... Use 'Root access' under 'Developer options' menu.

--

**RELEASE:** Tested after integrating new features, more stable than NIGHTLY. (Odexed builds)
**NIGHTLY:** Built daily with newest code and experimental features, might contain undiscovered bugs. (Deodexded builds)
**HISTORY:** Final odexded builds once a newer Android version is out and being built.
**EXPERIMENTAL:** Released when a new device is added or when a new feature is added for public beta testing and feedback. (Deodexded builds)
**UNOFFICIAL:** Maintained separately by individual developers, usually involves modification of shared code which cannot be merged (affects other devices), therefore maintained by the developer himself.

Yu Browser & Aegis - can be uninstalled through TitaniumBackup (then restart the device).

#twrp #cwm #customrom #stock #recovery #mokee #cyanogen #sammobile

origin - http://www.pipiscrew.com/?p=6092 samsung-tipsntricks