---
title: Encrypt Your Windows Pagefile To Improve Security
author: PipisCrew
date: 2017-11-24
categories: [news]
toc: true
---

https://www.ghacks.net/2011/04/04/encrypt-your-windows-pagefile-to-improve-security/

https://www.sevenforums.com/tutorials/143662-page-file-encryption-enable-disable.html

**<span style="color: #ff0000;">-or-</span>**

## Disable PageFile (pagefile.sys)

CPanel > System > Advanced system settings > click on the Advanced tab > Performance click > click on Settings > Advanced you will say that it says “Virtual memory and total paging file size for all drives” that is where you can **change Windows page file size** or instruct Windows not to use a page file at all. [ref1](https://www.howtogeek.com/95915/heres-why-disabling-the-windows-pagefile-is-pointless/)  [ref2](https://www.tweakhound.com/2011/10/10/the-windows-7-pagefile-and-running-without-one/)

## Disable Hibernation (hiberfil.sys)

open cmd as administrator

```js
//automatically deletes the hiberfil.sys
powercfg.exe /hibernate off

//to turn on
powercfg.exe /hibernate on
```

origin - http://www.pipiscrew.com/?p=11345 encrypt-your-windows-pagefile-to-improve-security