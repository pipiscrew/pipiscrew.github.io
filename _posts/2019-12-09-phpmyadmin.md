---
title: phpMyAdmin - Error Incorrect format parameter
author: PipisCrew
date: 2019-12-09
categories: [php]
toc: true
---

Change following in **php.ini**

```js
upload_max_filesize=64M
post_max_size=64M
```

src - https://stackoverflow.com/a/50746614/1320686

origin - https://www.pipiscrew.com/?p=16278 phpmyadmin-error-incorrect-format-parameter