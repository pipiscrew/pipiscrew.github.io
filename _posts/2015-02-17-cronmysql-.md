---
title: o[cron+mysql] schedule mysql backup through cron
author: PipisCrew
date: 2015-02-17
categories: []
toc: true
---

reference
[http://www.comentum.com/mysqldump-cron.html](http://www.comentum.com/mysqldump-cron.html)
[http://www.a2hosting.com/kb/developer-corner/mysql/mysql-database-backups-using-cron-jobs](http://www.a2hosting.com/kb/developer-corner/mysql/mysql-database-backups-using-cron-jobs)
[https://my.bluehost.com/cgi/help/168](http://my.bluehost.com/cgi/help/168)
**howto backup/restore through mysqldump** -[ http://blog.winhost.com/using-mysqldump-to-backup-and-restore-your-mysql-databasetables/]( http://blog.winhost.com/using-mysqldump-to-backup-and-restore-your-mysql-databasetables/)
**mysqldump-php** - [http://github.com/ifsnop/mysqldump-php](http://github.com/ifsnop/mysqldump-php)
**MySQL-Dump-with-Foreign-keys** - [http://github.com/dszymczuk/MySQL-Dump-with-Foreign-keys](http://github.com/dszymczuk/MySQL-Dump-with-Foreign-keys)
**shuttle-export** - [http://github.com/2createStudio/shuttle-export](http://github.com/2createStudio/shuttle-export)
php script - [http://davidwalsh.name/backup-mysql-database-php](http://davidwalsh.name/backup-mysql-database-php)

![](https://www.pipiscrew.com/wp-content/uploads/2015/02/snap485.png "snap485")

```jsmysqldump -u mysql_user -pmysql_password db_name > backup.sql```

![](https://www.pipiscrew.com/wp-content/uploads/2015/02/snap487.png "snap487")

* * *

when needed to create the backup file to a directory, this directory should have permissions **700**

```jsmysqldump -u mysql_user -pmysql_password db_name > mysql_backup/backup.sql```

![](https://www.pipiscrew.com/wp-content/uploads/2015/02/snap489.png "snap489")

* * *

> MajorLeo & Steven Westbrook wrote

If you want to create a backup to download it via the browser, you also can do this without using a file.
The php function **passthru()** will directly redirect the output of mysqldump to the browser. In this example it also will be zipped.
Pro: You don't have to deal with temp files.
Con: Won't work on Windows. May have limits with huge datasets.

```js
//http://stackoverflow.com/a/19575620
<?php $dbuser="user" ;="" $dbpasswd="password" ;="" $database="user_db" ;="" $filename="backup-" .="" date("d-m-y")="" .="" ".sql.gz";="" $mime="application/x-gzip" ;="" header(="" "content-type:="" "="" .="" $mime="" );="" header(="" 'content-disposition:="" attachment;="" filename="' . $filename . '" '="" );="" $cmd="mysqldump -u $DBUSER --password=$DBPASSWD $DATABASE | gzip --best" ;="" passthru(="" $cmd="" );="" exit(0);=""?>
```

origin - http://www.pipiscrew.com/?p=2424 cronmysql