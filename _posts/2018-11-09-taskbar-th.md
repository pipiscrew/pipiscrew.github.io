---
title: Taskbar Thumbnail Threshold to Show List
author: PipisCrew
date: 2018-11-09
categories: [news]
toc: true
---

The taskbar will only show thumbnails of so many opened windows or tabs for an item before the threshold is reached and will then automatically show a list afterwards for that item.

```js
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Taskband]
"NumThumbnails"=dword:00000000
```

to revert back to normal, delete the registry key created

src - https://www.tenforums.com/tutorials/20989-change-taskbar-thumbnail-threshold-show-list-windows-10-a.html

#win7 #win10

origin - http://www.pipiscrew.com/?p=6463 taskbar-thumbnail-threshold-to-show-list