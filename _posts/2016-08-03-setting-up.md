---
title: Setting Up a PHP job on Windows System
author: PipisCrew
date: 2016-08-03
categories: [php]
toc: true
---

source - http://stackoverflow.com/a/29044453
Open a command prompt and type

```js
schtasks /create /tn "XamppCron" /tr "L:\xampp\php\php.exe L:\xampp\htdocs\mydevsite\cron.php" /sc minute /mo 10
```

#schedule #cron

origin - http://www.pipiscrew.com/?p=5965 setting-up-a-php-job-on-windows-system