---
title: Visual Studio 2019 Community Offline Installation
author: PipisCrew
date: 2019-07-19
categories: [.net,va]
toc: true
---

1-Download [web installer](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16).

2-Open CMD execute the following :

```js
vs_community.exe --layout C:\vs2019 --add Microsoft.VisualStudio.Workload.CoreEditor --add Microsoft.VisualStudio.Workload.Data --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Microsoft.VisualStudio.Workload.Node --includeOptional --lang en-US
```

3-On 16/06/2019 dowloaded <span style="color: #ff0000;">**3.3GB**</span>, request only the following^ (find [out](https://docs.microsoft.com/en-us/visualstudio/install/workload-component-id-vs-community?vs-2019&view=vs-2019\)). MS claims full community setup is 35GB ;).

4-Goto&run **C:\vs2019\vs_setup.exe**

tested and working :

*   Winforms

*   NuGet

*   IIS Express

*   [angular](https://www.pipiscrew.com/2019/06/angular-v8-x-with-nodejs-hello-world/) v8.0 w/ TypeScript & nodeJS

*   ASP.NET WebAPI

Illustrated (default checked options, nothing extra downloaded by internet):
![](https://i.imgur.com/VsYjcGg.png)

![](https://i.imgur.com/FeAEHoM.png)

* * *

Entity is not installed :(
@VS, go to search bar, then type "Get tools and features" you can add or modify your features.
@ ASP.NET expand the tree check **Entity framework v6 tools** is 28mb.
src - https://stackoverflow.com/a/48513131

* * *

--

Step by step [https://gist.github.com/CHEF-KOCH/839542a8171bec07f5d62ae22c296101](https://gist.github.com/CHEF-KOCH/839542a8171bec07f5d62ae22c296101)

--

greets to [FastStone](https://www.faststone.org/FSCaptureDetail.htm) for the scrolling capture!

origin - https://www.pipiscrew.com/?p=15029 visual-studio-2019-community-offline-installation