---
title: redirect any request to specific file with htaccess
author: PipisCrew
date: 2016-10-05
categories: [news]
toc: true
---

create a file .htaccess to root

```js
RewriteEngine on
RewriteRule .* index.php [NC,L]
```

ref:
http://stackoverflow.com/questions/10740635/rewriterule-index-php-nc-l
http://stackoverflow.com/questions/2439562/apache-rewriterule-index-php-nc-l-not-working

origin - http://www.pipiscrew.com/?p=6163 redirect-any-request-to-specific-file-with-htaccess