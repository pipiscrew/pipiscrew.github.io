---
title: Cisco Webex Meetings
author: PipisCrew
date: 2020-03-30
categories: [news]
toc: true
---

So, today I received a WebEx invitation link, couldnt establish a connection a messagebox pops

    ---------------------------
    WebEx
    ---------------------------
    Failed to get correct parameters while downloading the meeting component. Contact Technical Support for assistance.
    ---------------------------
    OK   
    ---------------------------

guess what, following the KB article https://bit.ly/2Jo7uKj

goto Control Panel > Internet Options > Advanced tab, then check 

'Use **TLS 1.2**' 

box under Security

Click Apply and select OK > rebrowse to WebEx link.

**fixed!**

* * *

The installation of browser WebEx addon installs at :

    C:\Users\%username%\AppData\Local\WebEx
    C:\Program Files (x86)\WebEx

* * *

You can make a test WebEx at 
https://www.webex.com/test-meeting.html/

origin - https://www.pipiscrew.com/?p=17792 cisco-webex-meetings