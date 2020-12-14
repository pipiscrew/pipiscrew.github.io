---
title: Error Handling
author: PipisCrew
date: 2017-03-02
categories: [php]
toc: true
---

basically PHP has a function to set a user-defined function when error occured. Handling **fatal errors** is impossible in PHP v5.x.

```js
//example
<?php set_error_handler("myerrorhandler");="" .="" .="" .="" trigger="" error="" trigger_error("log(x)="" for="" x=""?><= 0="" is="" undefined,="" you="" used:="" scale="$scale"," e_user_error);="" function="" sendmail($recipient_mail,="" $subject,="" $body)="" {="" $headers="From: x@x.com\r\n" ;="" $headers="" .="MIME-Version: 1.0\r\n" ;="" $headers="" .="Content-Type: text/html; charset=utf-8\r\n" ;="" $message='' ;="" $message="" .="$body;" $message="" .='' ;="" line="" with="" trick="" -="" http://www.xpertdeveloper.com/2013/05/set-unicode-character-in-email-subject-php/="" $updated_subject="=?UTF-8?B?" .="" base64_encode($subject)="" .="" "?=";

    if (mail($recipient_mail, $updated_subject, $message, $headers)) {
      return true;
    } else {
      return false;
    }
}

// A user-defined error handler function - http://php.net/manual/en/function.set-error-handler.php
function myErrorHandler($errno, $errstr, $errfile, $errline)
{
    if (!(error_reporting() & $errno)) {
        // This error code is not included in error_reporting, so let it fall
        // through to the standard PHP error handler
        return false;
    }

    $mail_body=" ";="" switch="" ($errno)="" {="" case="" e_user_error:="" $mail_body="**My ERROR** [$errno] $errstr  
\n" ;="" $mail_body="" .="  Fatal error on line $errline in file $errfile" ;="" $mail_body="" .=", PHP " .="" php_version="" .="" "="" ("="" .="" php_os="" .="" ")="" \n";="" $mail_body="" .="Aborting...  
\n" ;="" exit(1);="" break;="" case="" e_user_warning:="" $mail_body="**My WARNING** [$errno] $errstr  
\n" ;="" break;="" case="" e_user_notice:="" $mail_body="**My NOTICE** [$errno] $errstr  
\n" ;="" break;="" default:="" $mail_body="Unknown error type: [$errno] $errstr  
\n" ;="" break;="" }="" sendmail("x@x.com",="" "error="" occured",="" $mail_body);="" *="" execute="" php="" internal="" error="" handler,="" otherwise="" return="" true,="" to="" continue="" the="" execution="" */="" return="" false;="" }="" ```="" example="" using="" the="" **set_error_handler**="" :="" http://www.w3schools.com/php/func_error_set_error_handler.asp=""  ="" *="" *="" *=""  ="" jdias="" said="" (2011)="" :=""></=>

> Actually you can handle parse and **fatal errors**. It is true that the error handler function you defined with set_error_handler() will not be called. The way to do it is by defining a shutdown function with register_shutdown_function().

src - http://stackoverflow.com/a/7313887

* * *

A long example (send mail on error) - http://nyphp.org/PHundamentals/7_PHP-Error-Handling
Customising the PHP error handler - https://www.tonymarston.net/php-mysql/errorhandler.html
How to perform error handling in PHP - https://web.stanford.edu/dept/its/communications/webservices/wiki/index.php/How_to_perform_error_handling_in_PHP

* * *

**whoops** is an error handler framework for PHP. Out-of-the-box, it provides a pretty error interface that helps you debug your web projects, but at heart it's a simple yet powerful stacked error handling system. **Dependencies required**
https://filp.github.io/whoops/

* * *

One file handling all (Kondrashov Ilia) - https://github.com/caseycs/php-error-handler

* * *

### In PHP v7.x

All **errors** in PHP 5 that were **fatal**, now throw instances of Error in PHP 7.

```js
try {

   // Code that may throw an Exception or Error.

} catch (Throwable $t) {

   // Executed only in PHP 7, will not match in PHP 5

} catch (Exception $e) {

   // Executed only in PHP 5, will not be reached in PHP 7

}
```

* * *

### Handling multiple exceptions in PHP 7.1

http://www.codediesel.com/php/handling-multiple-exceptions-in-php-7-1/

origin - http://www.pipiscrew.com/?p=6664 php-error-handling