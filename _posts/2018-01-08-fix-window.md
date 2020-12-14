---
title: Fix Windows 7 BSOD 0x000000c4 after installing KB4056894
author: PipisCrew
date: 2018-01-08
categories: [news]
toc: true
---

https://www.ghacks.net/2018/01/08/fix-windows-7-bsod-0x000000c4-after-installing-kb4056894/

-Use the F8-key during the boot sequence and select Repair Your Computer in the menu that pops up. If you have difficulties opening the menu hammer on the F8-key repeatedly until the menu appears.
-Open a command prompt window.
-Run dir d: to check that the Windows drive is mapped.
-Run dism /image:d:\ /remove-package /packagename:Package_for_RollupFix~31bf3856ad364e35~amd64~~7601.24002.1.4 /norestart

src - https://www.deskmodder.de/blog/2018/01/08/kb4056894-windows-7-startet-nach-update-nicht-mehr-bsod-loesung/

origin - http://www.pipiscrew.com/2018/01/fix-windows-7-bsod-0x000000c4-after-installing-kb4056894/ fix-windows-7-bsod-0x000000c4-after-installing-kb4056894