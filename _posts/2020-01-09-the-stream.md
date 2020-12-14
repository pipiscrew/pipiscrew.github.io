---
title: The stream or file -storage/laravel.log- could not be opened- failed to open stream- Permission denied
author: PipisCrew
date: 2020-01-09
categories: [php,docker]
toc: true
---

```js
# src - https://github.com/guillaumebriday/laravel-blog/issues/63

php artisan cache:clear
chmod -R 777 storage/
```

without docker - https://stackoverflow.com/a/49994594

origin - https://www.pipiscrew.com/?p=16533 the-stream-or-file-storagelaravel-log-could-not-be-opened-failed-to-open-stream-permission-denied