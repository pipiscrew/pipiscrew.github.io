---
title: o[php+mysql+apache] USBWebserver
author: PipisCrew
date: 2015-03-30
categories: []
toc: true
---

Is a combination of the popular webserver software: Apache, MySQL, Php and PhpMyAdmin. With USBWebserver it is possible to develop and show your php websites, everywhere and anytime The advantage of USBWebserver is, you can use it from USB of even CD

Features:

*   Show a offline version of your website

*   Anywhere and anytime develop php websites

*   No need for expensive hosting

*   Working at multiple locations at projects

*   A good test before putting your website online

<div>[http://www.usbwebserver.net](http://www.usbwebserver.net)</div>
<div>On pc2 (pc name: <span style="color: #ff0000;">**sales2**</span>) I install it^, didnt parameterize anything, just share the **root** folder cross network.</div>
<div>

On pc1 I browse at <span style="color: #ff0000;">**http://sales2:8080/**  <span style="color: #000000;">(by default listen to 8080) the predefined index.php appears! (aka root\index.php) </span></span>

<span style="color: #ff0000;"><span style="color: #000000;">On pc1 I browse at <span style="color: #ff0000;">**http://sales2:8080/phpmyadmin/** <span style="color: #000000;">using the following default credentials</span></span></span></span>

![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap400.png "snap400")

</div>

* * *

> No connection could be made because
>  the target machine actively refused it.

by default mySQL port is 3306, USBServer mySQL uses 3307 so on PHP mySQL connection we have to define the port! aka :

```js
//port
<?php $mysql_hostname="localhost:3307" ;="" $mysql_user="root" ;="" $mysql_password="usbw" ;="" $mysql_database="test_db" ;="" setup="" a="" connection="" with="" mysql="" $mysqli="new" mysqli($mysql_hostname,="" $mysql_user,="" $mysql_password,="" $mysql_database);=""?>
```

when using a desktop application use 127.0.0.1

* * *

On pc1 we should access mySQL running on pc2, by default the root user is limited for local access only, grant permissions via 

```jsGRANT ALL ON *.* to root@'192.168.1.%' IDENTIFIED BY 'usbw';```

source - [http://stackoverflow.com/a/11743058](http://stackoverflow.com/a/11743058)

* * *

by default PHP echo, the errors, you can stop it, go to  
D:\server\php\php.ini and set 
```jsdisplay_errors = Off```

then view the errors by :
![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap401.png "snap401") 

* * *

similar - http://www.mamp.info

origin - http://www.pipiscrew.com/?p=2293 phpmysqlapache-usbwebserver