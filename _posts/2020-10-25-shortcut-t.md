---
title: shortcut to disconnect connect from the network
author: PipisCrew
date: 2020-10-25
categories: [news]
toc: true
---

```js
netsh interface set interface name="Ethernet" admin=Disabled

netsh interface set interface name="Ethernet" admin=Enabled
```

create batch files, r-click each of, tab shortcut > advanced > "run as administrator" check it!

ref :
https://answers.microsoft.com/en-us/windows/forum/all/ethernet-disableenable-shortcut/c3215bbe-3d70-4151-89c1-0df43febdf5c
https://www.tenforums.com/network-sharing/44274-shortcut-enable-disable-network-wired.html

* * *

Change DNS Servers using the Command Prompt

```js
// src - https://helpdeskgeek.com/networking/change-ip-address-and-dns-servers-using-the-command-prompt/

//find you interface name (in below example we using 'Ethernet')
etsh interface ipv4 show config

//store that will use custom DNS
netsh interface ipv4 set dns name="Ethernet" static DNS_SERVER

//primary
netsh interface ipv4 set dns name="Ethernet" static 8.8.8.8

//secondary
netsh interface ipv4 set dns name="Ethernet" static 8.8.4.4 index=2
```

origin - https://www.pipiscrew.com/?p=14623 shortcut-to-disconnect-connect-from-the-network