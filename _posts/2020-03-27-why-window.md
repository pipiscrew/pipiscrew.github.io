---
title: Why Windows 95 and 98 would crash after 49.7 days of uptime
author: PipisCrew
date: 2020-03-27
categories: [news]
toc: true
---

Why Windows 95 and Windows 98 would crash after 49.7 days of uptime

There’s a famous bug in Windows 95 and Windows 98 (now patched) that caused these systems to stop functioning after 49.7 days of uptime. I used to wonder how this happened – in addition to wondering how many Windows 95 / 98 systems could achieve such uptimes to begin with!

Finally, I did a little math and figured out what must be behind this bug. It’s actually quite cute.

First, we need to know about a function called GetTickTime which is part of the Windows API. This function returns a DWORD value representing the number of milliseconds which has elapsed since the system has come up.

What’s a DWORD? A Word on an x86 is 16 bits, so a Double Word is 32 bits. The maximum number expressed in 32 bits is 2 to the power of 32.

2^32 = 4,294,967,296

We’re expressing a number of milliseconds here. How many milliseconds are there in one day?

(milliseconds per second) * (seconds per minute) * (minutes per hour) * (hours per day) = 1000 * 60 * 60 * 24 = 86,400,000.

Finally, we can find out how many days’ worth of milliseconds we can fit in the DWORD:

4,294,967,296 / 86,400,000 = 49.7102696

Voila! After 49.71 days

https://sites.google.com/site/edmarkovich2/whywindows95andwindows98wouldcrashafter49.7daysofuptime

origin - https://www.pipiscrew.com/?p=17703 why-windows-95-and-98-would-crash-after-49-7-days-of-uptime