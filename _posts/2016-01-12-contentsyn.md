---
title: ContentSync
author: PipisCrew
date: 2016-01-12
categories: [app,.net]
toc: true
---

Suppose you need to sync the contents of two large folders, Source and Destination. Normally robocopy *.* Source Destination /MIR does the job. However even if the byte content of a file didn't change, but the timestamp did, robocopy will copy the file and change the timestamp of the destination to match the source.

First it diffs the source and destination directories and builds a flat list of files 1) present only on the left, 2) present only on the right, 3) changed between left and right and 4) fully identical (having same bytes).

[https://github.com/KirillOsenkov/ContentSync](https://github.com/KirillOsenkov/ContentSync)

robocopy itself - [https://technet.microsoft.com/en-us/magazine/ee851678.aspx](https://technet.microsoft.com/en-us/magazine/ee851678.aspx)

origin - http://www.pipiscrew.com/?p=3159 app-contentsync