---
title: o[apache] htaccess
author: PipisCrew
date: 2015-08-29
categories: [Uncategorized]
toc: true
---

reference 
[http://gist.github.com/ScottPhillips/1721489](http://gist.github.com/ScottPhillips/1721489)

```js
//.htaccess - folder free - source http://community.sitepoint.com/t/setting-rewritebase-automatically-as-the-current-directory/2141/6
<ifmodule rewrite_module="">
AcceptPathInfo On

RewriteEngine On

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/?$1 [L]
</ifmodule>
```

when I hit http://x.com/blog
```js
//the x.com/index.php 
<?php var_dump($_get);="" ```="" outputs="" array(1)="" {="" ["blog"]=""?> string(0) "" }

* * *

> Building a basic router

[http://medium.com/@dylanbr/building-a-basic-router-b43c17361f8b](http://medium.com/@dylanbr/building-a-basic-router-b43c17361f8b)

ex.
http://example.com/this/is/the/route

```jsRewriteEngine On
RewriteRule ^(.*)$ index.php [NC,L]```

* * *

> Adding an Index.html Front Page to Forum

source - https://www.phpbb.com/community/viewtopic.php?p=13191070#p13191070

at the very top of the file on a line by itself, copy and paste this:

```jsDirectoryIndex home.html index.php```

now, what will happen is that when somebody visits your site at http://yourdomain.com they will automatically see the home.php page instead of the index.php

origin - http://www.pipiscrew.com/?p=3542 apache-htaccess