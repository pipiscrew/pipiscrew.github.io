---
title: Windows problem accessing share folder
author: PipisCrew
date: 2016-11-18
categories: [news]
toc: true
---

If suddenly the share folder you access for a long, stop working, you have to erase the credentials stored to your computer. One option is to do it by CPanel > Credential Manager, believe me tried, even deleted from there, couldnt access the folder. Deleting the stored credentials by the DOS **net use** command made the trick!

List all stored credentials -> `net use`

delete all the stored credentials -> `net use * /delete` or 
delete only the entry for a share `net use \\192.168.2.43\data /delete`

then you have to go to mycomputer choose 'map a drive' (maybe ‘Connect using different credentials’ is helpful)

## runas /user:myComputer\administrator "explorer /separate"</code>

origin - http://www.pipiscrew.com/?p=6269 windows-problem-accessing-share-folder