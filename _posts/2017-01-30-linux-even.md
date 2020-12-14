---
title: Linux Event Logs
author: PipisCrew
date: 2017-01-30
categories: [linux]
toc: true
---

Linux Log files and usage

=> /var/log/messages : General log messages
=> /var/log/boot : System boot log
=> /var/log/debug : Debugging log messages
=> /var/log/auth.log : User login and authentication logs
=> /var/log/daemon.log : Running services such as squid, ntpd and others log message to this file
=> /var/log/dmesg : Linux kernel ring buffer log
=> /var/log/dpkg.log : All binary package log includes package installation and other information
=> /var/log/faillog : User failed login log file
=> /var/log/kern.log : Kernel log file
=> /var/log/lpr.log : Printer log file
=> /var/log/mail.* : All mail server message log files
=> /var/log/mysql.* : MySQL server log file
=> /var/log/user.log : All userlevel logs
=> /var/log/xorg.0.log : X.org log file
=> /var/log/apache2/* : Apache web server log files directory
=> /var/log/lighttpd/* : Lighttpd web server log files directory
=> /var/log/fsck/* : fsck command log
=> /var/log/apport.log : Application crash report / log file

src - https://ubuntuforums.org/showthread.php?t=1568706&p=9810348#post9810348

origin - http://www.pipiscrew.com/?p=6552 linux-event-log