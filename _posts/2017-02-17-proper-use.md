---
title: proper use of spl_autoload_register and set_include_path
author: PipisCrew
date: 2017-02-17
categories: [php]
toc: true
---

If you have a several classes in your PHP project then you already know how annoying it can be to constantly include the class files before instantiating your class.  

PSR-0 compliant autoloader 

```js
//http://www.gingerframework.com/docs/getstarted.php

// Add the appropiate extra include paths here
$includePaths = array(
    __DIR__."/../vendor/",
    __DIR__."/../modules/"
);

// Add the above paths to the global include path
set_include_path(implode(PATH_SEPARATOR, $includePaths));

// Register the psr-0 autoloader for ease of use 
spl_autoload_register(function($c){@include preg_replace('#\\\|_(?!.+\\\)#','/',$c).'.php';}); 

// if needed, include the vendor/autoload.php for the composer packages
include 'autoload.php';
```

origin - http://www.pipiscrew.com/?p=6747 php-proper-use-of-spl_autoload_register-and-set_include_path