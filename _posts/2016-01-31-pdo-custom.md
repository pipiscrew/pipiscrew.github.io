---
title: PDO Custom Class
author: PipisCrew
date: 2016-01-31
categories: [php]
toc: true
---

PDO - PHP Data Objects - is a database access layer providing a uniform method of access to multiple databases.
Re-introducing PDO – the Right Way to Access Databases in PHP - [http://www.sitepoint.com/re-introducing-pdo-the-right-way-to-access-databases-in-php/](http://www.sitepoint.com/re-introducing-pdo-the-right-way-to-access-databases-in-php/)

Mysql Database access using PDO - [http://agalaxycode.blogspot.in/2015/10/mysql-database-access-using-pdo.html](http://agalaxycode.blogspot.in/2015/10/mysql-database-access-using-pdo.html)

Why you Should be using PHP's PDO for Database Access - [http://code.tutsplus.com/tutorials/why-you-should-be-using-phps-pdo-for-database-access--net-12059](http://code.tutsplus.com/tutorials/why-you-should-be-using-phps-pdo-for-database-access--net-12059)

The following database drivers are available:

<li>PDO_DBLIB ( FreeTDS / Microsoft SQL Server / Sybase )</li>
<li>PDO_FIREBIRD ( Firebird/Interbase 6 )</li>
<li>PDO_IBM ( IBM DB2 )</li>
<li>PDO_INFORMIX ( IBM Informix Dynamic Server )</li>
<li>PDO_MYSQL ( MySQL 3.x/4.x/5.x )</li>
<li>PDO_OCI ( Oracle Call Interface )</li>
<li>PDO_ODBC ( ODBC v3 (IBM DB2, unixODBC and win32 ODBC) )</li>
<li>PDO_PGSQL ( PostgreSQL )</li>
<li>PDO_SQLITE ( SQLite 3 and SQLite 2 )</li>
<li>PDO_4D ( 4D )</li>

All of these drivers are not necessarily available on your system; here's a quick way to find out which drivers you have:

```js
print_r(PDO::getAvailableDrivers());
```

```js
//config_pdo.php
<?php function="" connect_mysql()="" {="" $mysql_hostname="localhost" ;="" $mysql_user="x" ;="" $mysql_password="x" ;="" $mysql_database="x" ;="" $dbh="new" pdo("mysql:host="$mysql_hostname;dbname=$mysql_database" ,"="" $mysql_user,="" $mysql_password,="" array(="" pdo::attr_errmode=""?> PDO::ERRMODE_EXCEPTION,
    PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8"
  ));

  return $dbh;
}

function connect_sqlite() {
	//if doesnt exist, will created.
	$dbh = new PDO('sqlite:dbase.db');

	return $dbh;
}

function getScalar($db, $sql, $params) {
	if ($stmt = $db -> prepare($sql)) {

		$stmt->execute($params);

		return $stmt->fetchColumn();
	} else
		return 0;
}

function getRow($db, $sql, $params) {
	if ($stmt = $db -> prepare($sql)) {

		$stmt->execute($params);

		return $stmt->fetch();
	} else
		return 0;
}

function getSet($db, $sql, $params) {
	if ($stmt = $db -> prepare($sql)) {

		$stmt->execute($params);

		return $stmt->fetchAll(PDO::FETCH_ASSOC);
//		return $stmt->fetchAll();
	} else
		return 0;
}

function executeSQL($db, $sql, $params) {
	if ($stmt = $db -> prepare($sql)) {

		$stmt->execute($params);

		return $stmt->rowCount();
	} else
		return false;
}
?>
```

* * *

source - [http://stackoverflow.com/a/2418514/1320686](http://stackoverflow.com/a/2418514/1320686)

> When should I use require vs. include?
> When should I use require_once vs. require?

The answer to 1
The **require()** function is identical to **include()**, except that it handles errors differently. If an error occurs, the **include()** function generates a warning, but the script will continue execution. The **require()** generates a fatal error, and the script will stop.

The answer to 2
The **require_once()** statement is identical to **require()** except PHP will check if the file has already been included, and if so, not include (require) it again.

* * *

```js
//sample.php
<?php require_once("config_pdo.php");="" $db="connect_mysql();" $user_id="3;" $a="1;" $names="" ;="" example="" 1="" $rows="getSet($db," "select="" *="" from="" users="" where="" user_id=""?>? and user_is_active=?", array($user_id,$a)); //always pass as array, when not have parameters pass plain null

foreach($rows as $row) {
	$names .= $row['user_name'] . ", ";
}

//example 2
$field = = getScalar($db, "select user_working_hour_id from user_working_hours where date_end is null and user_id=? order by user_working_hour_id DESC limit 1",array($user_id));

if(!$field ) //when the variable is not filled
	echo "error";
else 
	echo $field;

//example 3
$row = getRow($db, "select * from user_working_hours where date_end is null and user_id=? order by user_working_hour_id DESC limit 1",array($user_id));

if(!$row)  //when the variable is not filled
	echo "error";
else 
	echo $r["user_working_hours_start"];
```

## Social Network with PHP and Laravel (AUG2015)

[https://www.youtube.com/playlist?list=PLfdtiltiRHWGGxaR6uFtwZnnbcXqyq8JD](https://www.youtube.com/playlist?list=PLfdtiltiRHWGGxaR6uFtwZnnbcXqyq8JD)

## Codecanyon - Simple Database Abstraction for PHP and MySQL

[http://codecanyon.net/item/simple-database-abstraction-for-php-and-mysql/](http://codecanyon.net/item/simple-database-abstraction-for-php-and-mysql/)

## Codecanyon - cQL - Best SQL (pdo - mysqli - mysql) Cache Class

[http://codecanyon.net/item/cql-best-sql-pdo-mysqli-mysql-cache-class/10102363](http://codecanyon.net/item/cql-best-sql-pdo-mysqli-mysql-cache-class/10102363)

origin - http://www.pipiscrew.com/?p=1526 php-pdo-custom-class