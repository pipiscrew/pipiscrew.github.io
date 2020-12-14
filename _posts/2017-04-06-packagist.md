---
title: Packagist
author: PipisCrew
date: 2017-04-06
categories: [php]
toc: true
---

Is the main Composer repository. It aggregates all sorts of PHP packages that are installable with [Composer](http://getcomposer.org).

[http://packagist.org/](http://packagist.org/)

### Guide for Windows installing dependencies for a downloaded application

1-download **composer.phar** by https://getcomposer.org/download/
2-put it near php.exe
3-extract the downloaded application to **htdocs**, this means that the **composer.json** is at \htdocs\composer.json and a \htdocs\lib created.
4-if you dont have git, download it from https://git-scm.com/download/win
5-keep in mind that php + git filepaths must be declared to cpanel > system > advanced sys settings > environment variables > to PATH (you must restart cmd window if is open)
6-goto **htdocs** and execute
```jsphp composer.phar install```
7-This will create the famous **vendor** directory, where stores all the dependencies for the downloaded application.
8-create a php file at \htdocs\index.php example :
```js
<?php require="" 'vendor/autoload.php';="" use="" selective\orm\database;="" $db="new" database('')="" or="" $db="new" \selective\orm\database(="" 'test',="" 'mysql',="" driver="" class="" ['host'=""?> 'localhost', 'username' => 'root', 'password' => 'password'] // MySQL driver parameters
);
```

### Possible errors

> PHP 7 download - The program can't start because VCRUNTIME140.dll is missing from your computer. Try reinstalling the program to fix this problem.

	https://www.microsoft.com/en-us/download/details.aspx?id=48145
	http://windows.php.net/downloads/releases/php-7.1.1-Win32-VC14-x86.zip

> The openssl extension is required for SSL/TLS protection but is not available

	open \php\php.ini make sure extension=php_openssl.dll is without semicolon

> Unable to load dynamic library 'C:\php\ext\php_openss l.dll' - The specified module could not be found.

	open \php\php.ini make sure extension_dir = "ext" is without semicolon

> Failed to clone https://github.com/phpredis/phpredis.git, git was not found, check that it is installed and in your PATH env.

	if git is installed delete the vendor folder from \php\ and retry
	1-if not download from https://git-scm.com/download/win
	2-add C:\Program Files (x86)\Git\bin or C:\Program Files (x86)\Git\cmd to your path (close dosbox and retry)

> 'composer' is not recognized as an internal or external command

create a batch file (near php.exe) **composer.bat** paste and save (restart of dosbox required) :

```js
//https://getcomposer.org/doc/00-intro.md#manual-installation
@php "%~dp0composer.phar" %*
```

test with
```js
composer --v```

### Install PHP7 and Composer on Windows 10

http://kizu514.com/blog/install-php7-and-composer-on-windows-10/

### Composer Vendor Directory Explained

https://tommcfarlin.com/the-vendor-directory/
https://igor.io/2013/09/04/composer-vendor-directory.html

### Search The PHP Package Repository

https://packagist.org/search/?tags=utf8

origin - http://www.pipiscrew.com/?p=1193 php-packagist