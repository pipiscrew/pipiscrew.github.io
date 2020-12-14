---
title: Dynamic DNS
author: PipisCrew
date: 2017-01-30
categories: [news,linux]
toc: true
---

Every computer attached to the Internet has an IP address. Name Translation is the process of relating a name (like 'www.google.com') to an IP address (like '74.125.19.103') so that a website (or other service) on a computer can be accessed using an easily remembered name, rather than the IP address number of the computer. Name Translation is implemented via a distributed database known as the Domain Name System.

http://www.dyndns.com/support/clients/
http://www.no-ip.com/getting_started.php
http://www.dynu.com/Free-Dynamic-DNS
http://www.easydns.com/dynamicdns.php3
http://www.zoneedit.com/doc/dynamic.html#faq1
http://www.dnspark.com/services/dynamicDNS.php
http://namecheap.simplekb.com/kb.show?show=article&articleid=583&categoryid=11
http://www.dslreports.com/faq/240
http://freedns.afraid.org/
http://opendns.org/
https://desec.io/
http://dnsmadeeasy.com/integration/dynamicdns/
https://now-ip.com/

src - https://help.ubuntu.com/community/DynamicDNS

### Configure Dyno with DDClient (third level hostname)

https://www.dynu.com/DynamicDNS/IPUpdateClient/DDClient

DDClient - To enable execution on startup, execute the following commands
```js
systemctl start ddclient.service
systemctl enable ddclient.service
```

remove DynDNS (dynupdater)
```js
sudo apt-get remove dynupdater
```

origin - http://www.pipiscrew.com/?p=6559 dynamic-dns