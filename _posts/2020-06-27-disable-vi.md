---
title: Disable Visual Studio Attach security warning when debugging IIS
author: PipisCrew
date: 2020-06-27
categories: [asp.net]
toc: true
---

![alt](https://i.imgur.com/XcPcZ2F.png)

<span style="color: #ff0000;">**2019 - 2017**</span>

1- Close Visual Studio 2019
2- Start **regedit.exe** and select the node **HKEY_USERS**
3- **File > Load Hive**, navigate to %localappdata%\Microsoft\VisualStudio\
you will see a folder writes a version ex **16.0_83f6bcec**, enter in, there you will
find <span style="background-color: #ffff00;">privateregistry.bin</span>, select it and click open.
4- Regedit will ask you for a **base name** (is temporary) so give anything like word **test**
5- you will find the key test @ **HKEY_USERS\test**, browse at
HKEY_USERS\test\Software\Microsoft\VisualStudio\16.0xxxxx\Debugger\
Create a new **DWORD (32bit)**, name it **DisableAttachSecurityWarning** and set the value to **1**.
6- Go back to tree and select the HKEY_USERS\**test**  then File > **Unload hive**

src - https://www.davici.nl/blog/disable-visual-studio-2019-iis-security-attach-warning
ref - https://stackoverflow.com/a/41122603

<span style="color: #ff0000;">**older**</span>

make sure Visual Studio is not running when changing the registry key or it will be overwritten on exit with the old value

Change (or create) the following registry key to 1:

```js
//Visual Studio 2008
HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\9.0\Debugger\DisableAttachSecurityWarning

//Visual Studio 2010
HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger\DisableAttachSecurityWarning

//Visual Studio 2012
HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\Debugger\DisableAttachSecurityWarning

//Visual Studio 2013
HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\12.0\Debugger\DisableAttachSecurityWarning

//Visual Studio 2015
HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\Debugger\DisableAttachSecurityWarning
```

src - https://stackoverflow.com/a/2026878

--

<span style="color: #ff0000;">**VS addons**</span>

[101,163 installs] [ReAttach](https://marketplace.visualstudio.com/items?itemName=ErlandR.ReAttach)
[5,970 installs] [Entrian Attach: Auto-Attach the debugger at process start](https://marketplace.visualstudio.com/items?itemName=EntrianSolutions-RichieHindle.EntrianAttachAuto-Attachthedebuggeratprocessstart) (paid)
[shortcut for old VS versions as Reattach on VS2019] [ Visual Commander](https://vlasovstudio.com/visual-commander/) ([howto](https://blog.markvincze.com/attach-to-process-shortcut-in-visual-studio/))

--

get reattach button to toolbar - https://stackoverflow.com/a/31649987

origin - https://www.pipiscrew.com/?p=18374 disable-visual-studio-attach-security-warning-when-debugging-iis