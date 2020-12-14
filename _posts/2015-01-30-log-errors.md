---
title: log errors to text
author: PipisCrew
date: 2015-01-30
categories: []
toc: true
---

source [http://perishablepress.com/advanced-php-error-handling-via-php/](http://perishablepress.com/advanced-php-error-handling-via-php/)
```js
//php.ini
;;; php error handling for production servers
display_startup_errors = off
display_errors = off
html_errors = off
log_errors = on
docref_root = 0
docref_ext = 0
error_log = /var/log/php/errors/php_error.log
```

OR on the PHP file :

```js
//http://stackoverflow.com/a/3531852
ini_set("log_errors", 1);
ini_set("error_log", "/tmp/php-error.log");
error_log( "Hello, errors!" );
Then watch the file:

tail -f /tmp/php-error.log
```

origin - http://www.pipiscrew.com/?p=2300 php-log-errors-to-text