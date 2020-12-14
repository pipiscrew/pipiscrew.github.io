---
title: Visual Studio Code w/ ftp-sync
author: PipisCrew
date: 2017-02-19
categories: [app,.net]
toc: true
---

[https://blogs.msdn.microsoft.com/nicktrog/2016/02/11/configuring-visual-studio-code-for-php-development/](https://blogs.msdn.microsoft.com/nicktrog/2016/02/11/configuring-visual-studio-code-for-php-development/)

## ftp-simple

the only with support **Remote directory open to workspace**
https://marketplace.visualstudio.com/items?itemName=humy2833.ftp-simple

tip : at output window choose ftp-simple to see the transactions!
- : doesnt compare the filedate

## ftp-sync

[https://marketplace.visualstudio.com/items?itemName=lukasz-wronski.ftp-sync](https://marketplace.visualstudio.com/items?itemName=lukasz-wronski.ftp-sync)

use Ctrl+Shift+P, write : ext install ftp-sync then
use again Ctrl+Shift+P type : ftp 

use:
ftp-sync: Init

to setup the plugin 

dont forget to set "uploadOnSave": true!
--

origin - http://www.pipiscrew.com/?p=5375 app-visual-studio-code-w-ftp-sync