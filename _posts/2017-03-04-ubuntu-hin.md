---
title: ubuntu hints-n-tips
author: PipisCrew
date: 2017-03-04
categories: [linux]
toc: true
---

reference 
[http://help.ubuntu.com/community/ExternalGuides](http://help.ubuntu.com/community/ExternalGuides)

[wine](https://www.winehq.org/) began in 1993 by Bob Amstadt as a way to support running Windows 3.1 programs on Linux

*   can run any WINDOWS program!! also .NET!!

*   can execute DOS BATCH script!!

*   has DOS prompt!!

steps :
download [rufus](https://rufus.akeo.ie/downloads/), point the .iso/img. say yes/ok to any messagebox.
install ubuntu
install wine via application center

download x86 distribution :
https://www.ubuntu.com/download/alternative-downloads
http://ftp.ntua.gr/pub/linux/ubuntu-releases/16.04/

download Lubuntu by http://lubuntu.me/

Install LXDE, a fast and light-weight GUI (when you have installed Ubuntu/CentOS minimal)
```js
sudo apt-get install lxde

##CentOS
yum install lxde

##ref https://wiki.lxde.org/en/Installation
```

* * *

> I cant find .wine folder under ~/.wine/ (aka home/username/.wine)

1-The Wine folder is hidden by default. To access it, open your Home folder and press Ctrl+H. This will show all the hidden folders
2-Run winecfg in a terminal - this will create the .wine folder in your home folder.
[http://askubuntu.com/a/67089](http://askubuntu.com/a/67089)
[http://askubuntu.com/a/264895](http://askubuntu.com/a/264895)

> Batch files not working!

1-goto terminal write "wine cmd.exe"
2-change dir to cd ~/.wine/drive_c/
and then then try to run your batch file from there!
[http://www.linuxforums.org/forum/red-hat-fedora-linux/112720-how-run-bat-files-wine.html](http://www.linuxforums.org/forum/red-hat-fedora-linux/112720-how-run-bat-files-wine.html)

* * *

> I got error moving file permission denied

Use nautilus, is the official file manager for the GNOME desktop.
Open Nautilus as sudo by typing **gksudo nautilus** in terminal
[http://askubuntu.com/a/24960](http://askubuntu.com/a/24960)

* * *

Download SRWARE deb and install it!

Instructions for 32 bit systems:
$ wget http://sourceforge.net/projects/srwareiron.mirror/files/SRWare%20Iron%2034.0.1850.0/iron.deb
$ sudo dpkg -i iron.deb

Instructions for 64 bit systems:
$ wget http://sourceforge.net/projects/srwareiron.mirror/files/SRWare%20Iron%2034.0.1850.0/iron64.deb
$ sudo dpkg -i iron64.deb

* * *

Autoload on startup

Open ~/.bashrc

Enter:
export JAVA_HOME="[replace with your path to the jdk]"
export PATH="$JAVA_HOME/bin:$PATH"

Restart the machine

* * *

> request root access

```js
sudo su
```

> for shutdown or restart

```jssudo poweroff
sudo reboot```

> delete a file

```js
rm wpa_supplicant.conf
```

> view the content of a file

```js
cat file.log
```

> Open terminal here

CTRL + ALT +T
then use sudo -i to grant root access

> Super key is

 Ctrl+Super (Super is the Windows key) 

> Linux Mint LAMP

http://community.linuxmint.com/tutorial/view/486

> Restore KDE Desktop

```jsplasma-desktop &```

> add repository & install emerald

source - [http://www.noobslab.com/2014/02/emerald-decorator-and-themes-available.html](http://www.noobslab.com/2014/02/emerald-decorator-and-themes-available.html)

```jssudo add-apt-repository ppa:noobslab/themes
sudo apt-get update
sudo apt-get install emerald compizconfig-settings-manager
```

restore unity!
[http://askubuntu.com/a/450433](http://askubuntu.com/a/450433)

* * *

> Lubuntu - Wake up from Suspend after lid close (fix black screen +10min)

enable and set ignore for HandleLidSwitch -> no work for me on LDXE (aka https://bugs.launchpad.net/ubuntu/+source/xfce4-power-manager/+bug/1222021)

no work either uninstall xfce4-power-manager and its dependencies
```js
sudo apt-get remove --auto-remove xfce4-power-manager
sudo apt-get purge --auto-remove xfce4-power-manager

##ref :
##http://askubuntu.com/a/520649
##http://installion.co.uk/ubuntu/precise/universe/x/xfce4-power-manager/uninstall/index.html
```

no solution found :(

[update] installing wattOSrev10x86 (http://planetwatt.com/) fixes the bug!

> How to add “Open terminal here” to Nautilus' context menu

```js
sudo apt-get install nautilus-open-terminal
```

then reset Nautilus :
```jsnautilus -q```

![](https://www.pipiscrew.com/wp-content/uploads/2015/01/Jph4X.png "Jph4X")

* * *

> application bandwidth limit

install it
```jssudo aptitude install trickle```

use :
trickle -u 10 -d 20 firefox
//or
trickle -u 50 firefox

^opens new instance

[http://linuxaria.com/article/manage-your-bandwidth-with-trickle](http://linuxaria.com/article/manage-your-bandwidth-with-trickle)

* * *

> Install UNRAR support to builtin app 'Archive Manager'

 sudo apt-get install unrar

or use *unp* command line [http://help.ubuntu.com/community/Unp](http://help.ubuntu.com/community/Unp)

> Install Qt runtimes

sudo apt-get install libqt4-*

> Find package name

[Applications -> Ubuntu Software Center ](http://askubuntu.com/questions/14649/how-can-i-find-the-name-of-a-package)  

[Debian Linux apt-get package management cheat sheet](http://www.cyberciti.biz/tips/linux-debian-package-management-cheat-sheet.html)

source - [http://askubuntu.com/a/216430](http://askubuntu.com/a/216430)
Check your **/etc/apt/sources.list**
**Update your apt**
sudo apt-get update

**Check if apt can find apache2**
sudo apt-cache search apache2

**Install apache2**
sudo apt-get install apache2

**Optional additional repositories**
Here are a few optional repos you can go ahead and add to the bottom of your sources.list.

#Chromium
deb http://ppa.launchpad.net/chromium-daily/stable/ubuntu precise main
deb-src http://ppa.launchpad.net/chromium-daily/stable/ubuntu precise main

> Allow execution of unknown .jar files

Right click filename.jar >
![](https://www.pipiscrew.com/wp-content/uploads/2015/01/1.png "1")
then double click it!

* * *

reference 
http://askubuntu.com/questions/362951/installed-teamviewer-using-a-64-bits-system-but-i-get-a-dependency-error
http://askubuntu.com/questions/40011/how-to-let-dpkg-i-install-dependencies-for-me

```js
//install once gdebi
sudo apt-get install gdebi-core

//download teamviewer
wget http://www.teamviewer.com/download/teamviewer_linux.deb

//install deb with dependencies
sudo gdebi teamviewer_linux.deb
```

* * *

## Install LAMP

reference https://www.howtoforge.com/ubuntu-lamp-server-with-apache2-php5-mysql-on-14.04-lts

warning for <strong style="color:red">phpmyadmin** https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-14-04
When the first prompt appears, apache2 is highlighted, but not selected. If you do not hit "SPACE" to select Apache, the installer will not move the necessary files during installation. Hit "SPACE", "TAB", and then "ENTER" to select Apache.
+
select yes when asked whether to use dbconfig-common to set up the database

*install apache2*
sudo apt-get install mysql-server mysql-client
sudo apt-get install apache2
surf @ http://0.0.0.0/ is alive!
sudo apt-get install php5 libapache2-mod-php5

*config server calling name*
edit the file 'apache2.conf' in /etc/apache2 add :
ServerName localhost

then restart the server
sudo service apache2 restart

*add php5 modules*
apt-get install php5-mysql php5-curl php5-gd php5-intl php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-snmp php5-sqlite php5-tidy php5-xmlrpc php5-xsl

*make php5 mcrypt module work*
sudo apt-get install mcrypt php5-mcrypt
sudo php5enmod mcrypt
sudo service apache2 restart

*change root dir*
http://stackoverflow.com/a/23175981/1320686

*remove apache2*
http://askubuntu.com/a/355256
sudo apt-get purge apache2

*remove phpmyadmin*
http://ubuntuforums.org/showthread.php?t=812971&p=5078918#post5078918
sudo apt-get --purge remove phpmyadmin

*use alias to server external dirs*
//http://stackoverflow.com/questions/13189261/apache2-alias-not-working-in-ubuntu
edit /etc/apache2/apache2.conf (this will add a directory demo) add:
```js
Alias /demo/ "/home/user/wwwb"
<directory "/home/user/wwwb"="">
    Order deny,allow
    AllowOverride All
	Require all granted
</directory>
```

## Configure a share folder to ubuntu w/ credentials

-the shared folder must be inside HOME folder
-as admin > edit /etc/samba/smb.conf add :

yourusername = current ubuntu user
```js
[nameit]
path=/home/yourusername/www
available=yes
valid users=yourusername
read only=no
browseable=yes
public=no
writable=yes
guest ok = no
```

save
-as admin execute
```jssmbpasswd -a yourusername```
when ask for user, type yourusername = current ubuntu user
when ask for password type a password will be used for SAMBA authentication

on windows side browse to ubuntu computer, you will see the shared folder, when ask for credentials
use for user ```jsubuntu_pc_name\yourusername``` 
for password the one you enter before. njoy!

reference
http://askubuntu.com/a/508702
net use * /d (restart required)
http://www.howtogeek.com/176471/how-to-share-files-between-windows-and-linux/

* * *

programs by category :
prefix rename - http://www.ubuntugeek.com/prefixsuffix-gui-application-that-renames-batches-of-files-in-ubuntu.html
samba server - samba
roboform for firefox/chrome (works with local passcards) - roboform website
screenrecording - http://www.maartenbaert.be/simplescreenrecorder/
free pascal - http://www.lazarus.freepascal.org/
[guide1] hardcode subtitles to mp4 - http://ubuntuforums.org/showthread.php?t=1848801
[guide2] hardcode subtitles to mp4 - http://goo.gl/gSv3g3

midnight commander (use CTRL+O to hide panels / F11 FullScreen)
```js
http://ftp.midnight-commander.org/?C=N;O=D

sudo apt-get install libglib2.0-dev
sudo apt-get install libslang2-dev

extract&compile&install, start with : mc
```

Krusader file manager - http://krusader.sourceforge.net/ or use ```jsapt-get install krusader```

Notepadqq is a native port of Notepad++ to Linux.
```js
//http://notepadqq.altervista.org/wp/
sudo add-apt-repository ppa:notepadqq-team/notepadqq
sudo apt-get update
sudo apt-get install notepadqq
```

Brackets IDE for web programming
```js
sudo add-apt-repository ppa:webupd8team/brackets
sudo apt-get update
sudo apt-get install brackets```

Deluge Torrent
```js
sudo apt-get install deluge
```

7zip
```js
sudo apt-get install p7zip-full

//split archive to multiparts 
7z -v100m a my_zip.7z my_folder/
```</strong>

origin - http://www.pipiscrew.com/?p=2282 ubuntu-hintsntips