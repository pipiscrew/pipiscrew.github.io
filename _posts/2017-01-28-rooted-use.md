---
title: rooted users modify GPS (NTP) servers
author: PipisCrew
date: 2017-01-28
categories: [android,news]
toc: true
---

Edit the **/system/etc/gps.conf** file.
The NTP server information is the part that you need to edit, to reflect NTP servers that are the nearest to you. As I am in the UK, I am using the uk.pool.ntp.org servers.

You will need to find out which are closest to your region, you can find out here http://www.pool.ntp.org/zone/

for europe use :
```js
//source - http://forum.xda-developers.com/showthread.php?t=939385
NTP_SERVER=europe.pool.ntp.org

//dont touch xtra_servers
xtra_server_1=http://xtra1.gpsonextra.net/xtra.bin
xtra_server_2=http://xtra2.gpsonextra.net/xtra.bin
xtra_server_3=http://xtra3.gpsonextra.net/xtra.bin

SUPL_HOST=supl.google.com
SUPL_PORT=7276
```

### How to flash modem only

![alt](http://imagizer.imageshack.com/img924/7545/Q4RUDD.jpg)

#gps #android

origin - http://www.pipiscrew.com/?p=6037 android-rooted-users-modify-gps-ntp-servers