---
title: call dotnet/com method on windows server only
author: PipisCrew
date: 2016-06-13
categories: [php,.net]
toc: true
---

The DOTNET class allows you to instantiate a class from a .Net assembly and call its methods and access its properties.

Once you have created a DOTNET object, PHP treats it identically to any other COM object; all the same rules apply.

```js
//http://php.net/manual/en/class.dotnet.php
//test_dotnet.php
<?php $stack="new" dotnet("mscorlib",="" "system.collections.stack");="" $stack-=""?>Push(".Net");
 $stack->Push("Hello ");
 echo $stack->Pop() . $stack->Pop();
?>
```

```js
//http://php.net/manual/en/class.com.php
//test_com.php
<?php $conn="new" com("adodb.connection")="" or="" die("cannot="" start="" ado");="" $conn-=""?>Open("Provider=SQLOLEDB; Data Source=localhost;
Initial Catalog=database; User ID=user; Password=password");

$rs = $conn->Execute("SELECT * FROM sometable");    // Recordset

$num_columns = $rs->Fields->Count();
echo $num_columns . "\n";

for ($i=0; $i < $num_columns;="" $i++)="" {="" $fld[$i]="$rs-">Fields($i);
}

$rowcount = 0;
while (!$rs->EOF) {
    for ($i=0; $i < $num_columns;="" $i++)="" {="" echo="" $fld[$i]-="">value . "\t";
    }
    echo "\n";
    $rowcount++;            // increments rowcount
    $rs->MoveNext();
}

$rs->Close();
$conn->Close();

$rs = null;
$conn = null;

?>
```

-Enable it in php.ini if dll exists - extension=php_com_dotnet.dll
-Once done RESTART the server.

The <span style='color:red'>DOTNET/COM</span> library in PHP is a part of the Windows Only Extensions - [http://is.php.net/manual/en/refs.utilspec.windows.php](http://is.php.net/manual/en/refs.utilspec.windows.php)

similar - [https://www.pipiscrew.com/2016/01/php-calling-cc-library-function/](https://www.pipiscrew.com/2016/01/php-calling-cc-library-function/)

similar - [PHP 5.x - SmartFTP Library Sample](https://www.smartftp.com/ftplib/samples/show?l=php&file=ftp%2FReadDirectory.phps)

* * *

## NetPhp

Using .Net code from PHP needs not to be a nightmare any more! Built upon the com_dotnet exten

-Use any .Net binaries (even without COM Visibility).
-Write code in PHP that consumes any of the .Net Framework libraries out of the box.
-Automatically generated PHP class dumps for IDE integration.
-Iterate over .Net collections directly from PHP.
-Propagation of .Net errors into native PHP exceptions that can be properly handled and examin
-Acces native enums and static methods.
-Use class constructors with parameters.
-Debug .Net and PHP code at the same time as if it was a single application.
-Works with libraries compiled for any version of the .Net framework (including 4.0 and above)

homepage :
http://www.drupalonwindows.com/en/content/netphp

test binaries :
http://www.drupalonwindows.com/sites/default/files/netphp2_0_0_4.zip

samples :
https://github.com/david-garcia-garcia/netphp

* * *

## PHP-DotNet-Bridge

[https://github.com/EionRobb/PHP-DotNet-Bridge](https://github.com/EionRobb/PHP-DotNet-Bridge)

Handling .NET assemblies in PHP
[http://blog.zitec.com/2012/handling-net-assemblies-in-php/](http://blog.zitec.com/2012/handling-net-assemblies-in-php/)

VB6 activex
[http://stackoverflow.com/a/1955456](http://stackoverflow.com/a/1955456)

origin - http://www.pipiscrew.com/?p=3371 php-call-dotnet-method