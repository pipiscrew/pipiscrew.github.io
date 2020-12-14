---
title: PHP developers in Ubuntu
author: PipisCrew
date: 2017-01-30
categories: [linux]
toc: true
---

To convert your **Ubuntu v14.04** into a powerhouse for PHP development , you need to install some developer tools from the rich set of available software packages. He (Maurits) made a top 10!

[http://www.leaseweblabs.com/2014/04/10-developer-tools-install-ubuntu-14-04/](http://www.leaseweblabs.com/2014/04/10-developer-tools-install-ubuntu-14-04/)

* * *

If you're a php developer on ubuntu, there comes the time where you have to install/reinstall your system. He (DaRaFF) did it already a few times and i decided to write down the steps for a typical web developer stack with php. 

[http://gist.github.com/DaRaFF/3995789](http://gist.github.com/DaRaFF/3995789)

* * *

The **XAMPP**  [http://www.apachefriends.org/index.html](http://www.apachefriends.org/index.html) [howto](http://ubuntuportal.com/2013/12/how-to-install-xampp-1-8-3-for-linux-in-ubuntu-desktop.html) install is supposed to be portable and can be started and stoped easily when required. It also has different security settings and come ready configured with extra tools (includes perl). However it's not good to use it for public web servers only for development and testing.
The **LAMP system** (aka **L**inux, **A**pache, **M**ySQL, **P**HP) [howto](http://howto.blbosti.com/2010/02/4-easiest-ways-to-install-lamp-server-on-ubuntu/) includes the same basic compnonent (Apache, MySQL and PHP) can be more difficult to configure. It can be more secure, easier to update and can be used for public webserve

* * *

Bluefish is a powerful editor targeted towards programmers and webdevelopers,
[http://bluefish.openoffice.nl/features.html](http://bluefish.openoffice.nl/features.html)

Aptitude is no longer installed by default on the recent releases of the Ubuntu family. 
You have to install :
```jssudo apt-get install aptitude```

Install bluefish :
```jssudo apt-get install bluefish
sudo aptitude install bluefish```

in general, to edit online files (ftp), use the **gvfs** 
installation :
```jssudo apt-get install gvfs```

then mount like :
```jsgvfs-mount "ftp://anonymous@ftp.symantec.com/"```

which appears at :
![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap324.png "snap324")

unmount like :
```jsgvfs-mount -u "ftp://anonymous@ftp.symantec.com/"```

is also curlftpfs [http://askubuntu.com/a/168350](http://askubuntu.com/a/168350)

* * *

**jEdit** Is a mature programmer's text editor with hundreds (counting the time developing plugins) of person-years of development behind it.

[http://www.jedit.org/](http://www.jedit.org/)
[jEdit - FTP Plugin](http://plugins.jedit.org/plugins/?FTP)
[jEdit - Plugin Central/](http://sourceforge.net/projects/jedit-plugins/)

1-You need to set the JAVA_HOME environment variable

2-install 'OpenJDK Java 6 runtime'
terminal > whereis java

ex. export JAVA_HOME=/usr/

origin - http://www.pipiscrew.com/?p=2261 php-developers-in-ubuntu