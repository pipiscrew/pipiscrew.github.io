---
title: Query Active Directory Without Writing a Script
author: PipisCrew
date: 2017-08-03
categories: [news]
toc: true
---

running this from the dos prompt
```jsRundll32 dsquery.dll OpenQueryWindow
```
will bring the Active Directory query window. Select the first user, use shift and select the last user > right click.

## Find name of Active Directory domain controller

```js//src - https://serverfault.com/a/718663
nltest /dclist:domainname
```
replace 'domainname' with your domain

Domain can be found under CPanel > System > Workgroup Settings

## Making Active Directory jQuery-easy

[https://github.com/dthree/ad/](https://github.com/dthree/ad/)

## SysExporter v1.75 - Export data from Windows controls

[http://www.nirsoft.net/utils/sysexp.html](http://www.nirsoft.net/utils/sysexp.html)

origin - http://www.pipiscrew.com/?p=9621 query-active-directory-without-writing-a-script