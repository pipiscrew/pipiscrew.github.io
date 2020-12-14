---
title: include_path
author: PipisCrew
date: 2017-02-06
categories: [php]
toc: true
---

**include_path string**
Specifies a list of directories where the require, include, fopen(), file(), readfile() and file_get_contents() functions look for files. The format is **like the system's PATH environment variable**: a list of directories separated with a colon in Unix or semicolon in Windows.

```js
set_include_path(get_include_path() . PATH_SEPARATOR . '/path/to/lib/'); //x.php belong here

//use of
require_once 'x.php';
```

origin - http://www.pipiscrew.com/?p=6643 php-include_path