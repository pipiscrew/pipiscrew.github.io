---
title: PHP Connect to Oracle
author: PipisCrew
date: 2017-02-06
categories: [php]
toc: true
---

enable php_pdo_oci.dll in **php.ini**

```js
function connect_oracle() {
	//enable ext - php_pdo_oci.dll
	//src - http://stackoverflow.com/a/36639484 -- https://www.devside.net/wamp-server/connect-wamp-server-to-oracle-with-php-php_oci8_11g-dll
	$server         = "127.0.0.1";
	$db_username    = "SYSTEM";
	$db_password    = "Oracle_1";
	$sid            = "ORCL";
	$port           = 1521;
	$dbtns          = "(DESCRIPTION=(ADDRESS_LIST = (ADDRESS = (PROTOCOL = TCP)(HOST = {$server})(PORT = {$port})))(CONNECT_DATA=(SID={$sid})))";
	$dbh = new PDO("oci:dbname=" . $dbtns . ";charset=utf8", $db_username, $db_password, array(
		PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
		PDO::ATTR_EMULATE_PREPARES => false,
		PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC));

	 return $dbh;
}
```

origin - http://www.pipiscrew.com/?p=6639 php-connect-to-oracle