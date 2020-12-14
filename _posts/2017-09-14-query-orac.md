---
title: query Oracle date field
author: PipisCrew
date: 2017-09-14
categories: [php,sql]
toc: true
---

The same query running on .NET application successfully, on PHP using PDO I got the error message : 

> Fatal error: Uncaught exception 'PDOException' with message 'SQLSTATE[HY000]: General error: 1858 OCIStmtExecute: ORA-01858: a non-numeric character was found where a numeric was expected (ext\pdo_oci\oci_statement.c:148)' in C:\x\htdocs\general.php:84 Stack trace: #0 C:\x\htdocs\general.php(84): PDOStatement->execute(NULL) #1 C:\x\htdocs\index.php(31): dbase->getSet('select NUMBERPR...', NULL) #2 {main} thrown in C:\x\htdocs\general.php on line 84

```js
$today = date("d-M-Y");     

$three_months_back = date('d-M-Y', strtotime("-90 days"));

$q =("select * from owner.table where 1=1 and ((close_date between '{$three_months_back}'
 and '{$today}') or (update_date between '{$three_months_back}' and '{$today}'))");
```

solution -> you must use the Oracle function **TO_DATE**

```js
--src - http://stackoverflow.com/a/17478514

$q =("select * from owner.table where 1=1 and ((close_date between TO_DATE('01-Jun-17','dd-MON-yy') 
and 
TO_DATE('31-Aug-2017','dd-MON-yy')) or (update_date between 
TO_DATE('01-Jun-17','dd-MON-yy') and TO_DATE('31-Aug-2017','dd-MON-yy'))");
```

origin - http://www.pipiscrew.com/?p=6668 php-query-oracle-date-field