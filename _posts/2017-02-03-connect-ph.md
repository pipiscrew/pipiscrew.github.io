---
title: Connect PHP with Oracle database
author: PipisCrew
date: 2017-02-03
categories: [php]
toc: true
---

TNS at C:\oracle\product\x\db_1\NETWORK\ADMIN

```js
//http://stackoverflow.com/a/5947976
<?php
    $db = "(DESCRIPTION=(ADDRESS_LIST = (ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.1.34)(PORT = 1521)))(CONNECT_DATA=(SID=orcl)))" ;

    if($c = OCILogon("system", "your database password", $db))
    {
        echo “Successfully connected to Oracle.\n”;
        OCILogoff($c);
    }
    else
    {
        $err = OCIError();
        echo “Connection failed.” . $err[text];
    }
?>
```

origin - http://www.pipiscrew.com/?p=6618 connect-php-with-oracle-database