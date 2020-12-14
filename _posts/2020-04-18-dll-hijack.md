---
title: DLL hijacking vulnerabilities in Nirsoft tools
author: PipisCrew
date: 2020-04-18
categories: [news]
toc: true
---

[German]The Nirsoft tools are probably known to many Windows users. What is less known: The tools come along with nasty DLL hijacking vulnerabilities and should rather be avoided. The topic has been bogged down here for quite some time and I have put it off again and again.

http://borncity.com/win/2020/04/16/dll-hijacking-vulnerabilities-in-nirsoft-tools/

* * *

Pretty much every single application made for Windows is "vulnerable" to this. It's not unique or special to Nirsoft tools. This is a common method of DLL injection for things such as games, or hot-patching for various libraries such as runtimes and such known as proxying. Some common targeted libraries are usually things like:

Direct3D: d3d8.dll, d3d9.dll, dinput.dll, ddraw.dll
Windows: wsock32.dll, version.dll, uxtheme.dll
Runtimes: msvcrt libraries, etc.

This is simply due to how the load order works on Windows in general. 

ref - https://docs.microsoft.com/en-us/windows/win32/dlls/dynamic-link-library-search-order

* * *

Dwmapi.dll abuse is a well known issue, the earliest report I could find, dates back to 2010: https://www.exploit-db.com/exploits/14734

It's trivial to solve using undocumented directive "loadFrom" in the application manifest file. ex 
https://github.com/curl/curl/issues/2326
[https://www.reddit.com/r/lowlevel/comments/4lktyw/sxs_backdoor_and_story_of_windows_uac_ridiculous/d3swp30/](https://www.reddit.com/r/lowlevel/comments/4lktyw/sxs_backdoor_and_story_of_windows_uac_ridiculous/d3swp30/)

origin - https://www.pipiscrew.com/2020/04/dll-hijacking-vulnerabilities-in-nirsoft-tools/ dll-hijacking-vulnerabilities-in-nirsoft-tools