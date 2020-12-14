---
title: Install Windows 10 directly without upgrade
author: PipisCrew
date: 2015-09-01
categories: [news]
toc: true
---

Here is what you need to do to clean install Windows 10 on a computer system.

You need a Windows 10 DVD or ISO image for that. If you don't have one get it from here. Download the tool from Microsoft's website to create the ISO image. Make sure you pick the right architecture and version.
Burn the ISO, mount it or extract it.
Navigate to the folder \Windows\x64\sources or P:\Windows\x32\sources and drag&drop the file gatherosstate.exe to the desktop.
Run the file afterwards. It creates GenuineTicket.xml on the desktop. This file is needed so copy it to a USB drive or other location.
Run a clean install of Windows 10 afterwards on the system. Make sure you skip the product key.
Once you are done and in Windows 10, copy the file GenuineTicket.xml to C:\ProgramData\Microsoft\Windows\ClipSVC\GenuineTicket.
The folder is hidden by default. If you cannot see it, select File > Options > View > Show hidden files, folders and drives in File Explorer.
Reboot the PC.
The next time you boot into Windows 10 it should be fully activated. You can verify that easily with a tap on Windows-Pause. This opens the System Control panel and the system's activation status at the bottom of the page.

[http://www.ghacks.net/2015/08/30/how-to-clean-install-windows-10-directly-without-upgrade/](http://www.ghacks.net/2015/08/30/how-to-clean-install-windows-10-directly-without-upgrade/)

origin - http://www.pipiscrew.com/?p=1796 install-windows-10-directly-without-upgrade