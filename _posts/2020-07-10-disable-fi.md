---
title: Disable Filezilla updates
author: PipisCrew
date: 2020-07-10
categories: [news]
toc: true
---

```js
-close application
-goto %appdata%\FileZilla
-delete filezilla.xml
-goto C:\Windows\System32\drivers\etc
-edit 'hosts' file, append :
127.0.0.1 update.filezilla-project.org
-save
```

if you like dont delete the filezilla.xml, edit it and remove this line 

![](https://i.imgur.com/Fk4mfIl.png)

src - [https://geektnt.com/how-to-disable-filezilla-update-nag-screen.html](https://geektnt.com/how-to-disable-filezilla-update-nag-screen.html)

origin - https://www.pipiscrew.com/?p=15327 disable-filezilla-updates