---
title: Visual Studio does not let me drag drop items into it?
author: PipisCrew
date: 2019-01-31
categories: [.net]
toc: true
---

If you **disable UAC** completely you can drag & drop from anywhere again. To do this you **can't use the slider in the Control Panel** because that only brings the UAC level down to **1**. Make this **registry change, reboot**, and you can again use your computer like god intended.

```js
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System]
"EnableLUA"=dword:00000000
```

ref - https://stackoverflow.com/a/30281987

ref powershell - https://social.technet.microsoft.com/Forums/windowsserver/en-US/0aeac9d8-3591-4294-b13e-825705b27730/how-to-disable-uac

origin - https://www.pipiscrew.com/?p=14668 visual-studio-does-not-let-me-drag-drop-items-into-it