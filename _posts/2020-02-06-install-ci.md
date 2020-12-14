---
title: Install Cinnamon Desktop Environment on Fedora v31
author: PipisCrew
date: 2020-02-06
categories: [linux]
toc: true
---

```js
//227 packages installed ~400mb

sudo dnf -y group install "Cinnamon Desktop"
```

reboot 

![alt](https://i.imgur.com/PBGapXw.png)

src - https://computingforgeeks.com/how-to-install-cinnamon-desktop-environment-fedora/

* * *

Remove Cinnamon Desktop

```js
//src - https://unix.stackexchange.com/a/520240

//avoid file conflicts
sudo dnf swap @cinnamon-desktop @gnome-desktop

//uninstall
sudo dnf -y group remove "Cinnamon Desktop"
```

* * *

## Install only Nemo File Manager w/o Cinnamon Desktop

```js
sudo dnf install nemo

//then search for application (gnome shell extension)
Toggle nemo

use Super+E to get a nemo window

//or use menulibre or alacarte
//https://louischristopher.me/setting-nemo-as-the-default-file-manager-in-fedora-23
//https://pkgs.org/download/menulibre
```

install nemo file roller (archive manager) 
```js
sudo dnf install nemo-fileroller
```

add 'extract here' option to file context menu (when you right click a compressed file)
-goto /usr/share/nemo/actions
-create a new file, name it extracthere.nemo_action
-paste the following :

```js
// https://askubuntu.com/a/578280

[Nemo Action]
Active=true
Name=Extract here
Comment=Extract here
Exec=file-roller -h %F
Icon-Name=gnome-mime-application-x-compress
 #Stock-Id=gtk-cdrom
Selection=Any
Extensions=zip;7z;ar;cbz;cpio;exe;iso;jar;tar;tar;7z;tar.Z;tar.bz2;tar.gz;tar.lz;tar.lzma;tar.xz;
```

-save it, restart the OS

made needed to create the file to another location and copy or move it there, due permissions :
```js
//move
mv /full/path/to/extracthere.nemo_action/usr

//copy
cp /full/path/to/extracthere.nemo_action/usr
```

[30 File Managers for Linux Systems](https://www.tecmint.com/top-best-lightweight-linux-file-managers/)

origin - https://www.pipiscrew.com/?p=16688 install-cinnamon-desktop-environment-on-fedora-v31