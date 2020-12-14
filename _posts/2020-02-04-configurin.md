---
title: Configuring Xorg as the default GNOME session
author: PipisCrew
date: 2020-02-04
categories: [Uncategorized]
toc: true
---

To run GNOME in X11, click the gear icon on the Fedora log in screen and select GNOME on Xorg, or complete the following steps:

Procedure:
1-Open /etc/gdm/custom.conf and uncomment WaylandEnable=false.

2-Add the following line to the [daemon] section:

```js
DefaultSession=gnome-xorg.desktop
```

3-Save the custom.conf file.

https://docs.fedoraproject.org/en-US/quick-docs/configuring-xorg-as-default-gnome-session/

origin - https://www.pipiscrew.com/?p=16707 configuring-xorg-as-the-default-gnome-session