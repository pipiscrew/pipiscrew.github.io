---
title: Install IIS on Windows 7
author: PipisCrew
date: 2015-12-04
categories: [news,asp.net]
toc: true
---

[http://www.codeproject.com/Tips/365704/Install-IIS-on-Windows](http://www.codeproject.com/Tips/365704/Install-IIS-on-Windows)

Now you can use Internet Information Services Manager to manage and configure IIS. To open IIS Manager, click Start, type **inetmgr** in the Search Programs and Files box, and then press Enter.

Make it public accessible  :
First you have to know the port on which your site is running. Usually your address is like 127.0.0.1:82, 82 being the port number. If is nothing it may be 80. To be sure, 
-go to IIS manager, 
-in the left expand Sites, right click on your site
-Edit Bindings, and you will see the port no.

Then
-Go to CP -> Windows Firewall
-Advanced settings
-Inbound Rules
-New Rule... 
-Select port
-TCP, your port number and a name. Also make sure that if you have another firewall, add an exception for it too, or disable it.

source [http://stackoverflow.com/a/10227246/1320686](http://stackoverflow.com/a/10227246/1320686)

## How to Setup IIS 6.0 on Windows 7 to Allow Classic ASP Sites to Run

[http://www.codeproject.com/Articles/43132/How-to-Setup-IIS-on-Windows-to-Allow-Classic](http://www.codeproject.com/Articles/43132/How-to-Setup-IIS-on-Windows-to-Allow-Classic)

origin - http://www.pipiscrew.com/?p=2232 install-iis-on-windows-7