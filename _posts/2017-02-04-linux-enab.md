---
title: Linux enable wifi connection on command prompt
author: PipisCrew
date: 2017-02-04
categories: [linux]
toc: true
---

iwconfig command is only to use only for WEP password, use it only to list the interfaces (http://superuser.com/a/353818)
for WPA2 use wpa_supplicant + wpa_passphrase instead (http://askubuntu.com/a/417498)

Guide connect to WPA2 wifi
```js
//src - https://gist.github.com/paulborza/d5799b53ae9c8dc6d62b36a252b32795
//tested & working

//get the name of the network interface
iwconfig

//edit file /etc/network/interfaces with vi command
//edit via > press i to insert text. 
//merge :
auto wlp1s0
iface wlp1s0 inet dhcp
wpa-ssid WIFI_NETWORK_NAME
wpa-psk WIFI_NETWORK_PASSWORD
//save via > press [Esc] type ZZ.

//enable connection via :
ifup -v wlp1s0
//test with ping google.com
```

you can find #install LXDE from commandline# at https://www.pipiscrew.com/2015/01/ubuntu-hintsntips/

#ubuntu

origin - http://www.pipiscrew.com/?p=6548 linux-enable-wifi-connection-on-command-prompt