---
title: Install VSFTPD server on Ubuntu 16.04 LTS
author: PipisCrew
date: 2017-02-04
categories: [linux]
toc: true
---

Some popular FTP sites for Debian, FreeBSD, RED HAT, SUSE, Kernel, KDE, GENOME etc., are powered by VSFTPD. It is the default FTP server for most Linux and Unix operating systems such as Red Hat, CentOS, Fedora, and Ubuntu.

https://www.ostechnix.com/install-vsftpd-server-ubuntu-16-04-lts/

```js
##update the package lists with : sudo apt-get update
sudo apt-get install vsftpd
sudo nano /etc/vsftpd.conf
```

Find and change the following lines as shown below.
```js
##Disable anonymous user login.
anonymous_enable=NO

##Uncomment these two lines.
ascii_upload_enable=YES
ascii_download_enable=YES

##Uncomment and enter your Welcome message - Not necessary, It's optional.
ftpd_banner=Welcome to OSTechNix FTP service.

##Add this line the end.
use_localtime=YES

# Uncomment this to enable any form of FTP write command.
write_enable=YES
```

restart the vsftpd service
```jssudo systemctl restart vsftpd
or
sudo service vsftpd restart```

check the satus via :
```js
sudo systemctl status vsftpd
```

you can use any linux account as ftp credential

### Change user directory

create a file under :
/var/www/userconfigs/**replace_user_name** (ex /var/www/userconfigs/costas)

edit **replace_user_name** file with the dir you want ex :
```js 
local_root=/var/www
```

goto /etc/vsftpd.conf and add this line :
```js
user_config_dir=/var/www/userconfigs

# Uncomment this to enable any form of FTP write command.
write_enable=YES
```

when you are under /var/ , make www dir writable with
```jschmod -R 777 www```

restart the vsftpd service (on the test needed 3times, till change)
```jssudo systemctl restart vsftpd```

ps the path **/var/www/userconfigs**  can be anywhere

* * *

add virtual users : https://www.reddit.com/r/linuxadmin/comments/5nm2qg/chroot_local_vsftpd_users_into_their_own/
http://askubuntu.com/a/784960
http://askubuntu.com/questions/73323/how-to-setup-vsftpd-for-multiple-users-including-adding-specific-directories
http://howto.gumph.org/content/setup-virtual-users-and-directories-in-vsftpd/
http://unix.stackexchange.com/questions/94603/limit-ftp-access-only-to-the-var-www-with-vsftpd

### ProFTPD

howto - http://www.tecmint.com/install-proftpd-in-ubuntu-and-debian/
homepage - http://www.proftpd.org/

origin - http://www.pipiscrew.com/?p=6632 install-vsftpd-server-on-ubuntu-16-04-lts