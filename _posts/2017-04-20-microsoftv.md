---
title: Microsoft.Visual Studio 2017 - Create offline installer
author: PipisCrew
date: 2017-04-20
categories: [news,.net]
toc: true
---

If you run it without arguments, will download ~20GB, the solution is to create and offline installer and go with it.

download 1mb community installer via https://www.visualstudio.com/

**the best ~2GB**
```js
//install NetCoreTools - then select what you want to install

vs_community.exe --layout c:\vs2017offline --lang en-US --add Microsoft.VisualStudio.Workload.NetCoreTools
```

**1.85GB** downloaded and still needs Internet Connection :
```js
//cmd by RolandCooper7 for Desktop & Web & NetCoreTools installation

vs_community.exe --layout c:\vs2017offline --lang en-US --includeRecommended --includeOptional --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetCoreTools --add Microsoft.VisualStudio.Workload.NetWeb
```

maybe is time for desktop devs try SharpDevelop - http://www.icsharpcode.net/

origin - http://www.pipiscrew.com/?p=7651 microsoft-visual-studio-2017-create-offline-installer