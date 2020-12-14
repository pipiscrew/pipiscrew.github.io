---
title: VirtualBox mount windows shared folder to linux
author: PipisCrew
date: 2017-11-05
categories: [linux]
toc: true
---

1-Share the windows folder through 'Devices > Shared folders'
2-Install Guest Additions through 'Devices > Insert Guest Additions CD Image'
3-Open terminal and execute :

```js
sudo mount -t vboxsf yoursharedfoldername ~/Public
```

4-Open your file manager, and you should see the contents of ~/Public

src - https://www.techrepublic.com/article/how-to-share-folders-between-guest-and-host-in-virtualbox/

origin - http://www.pipiscrew.com/?p=11000 virtualbox-mount-windows-shared-folder-to-linux