---
title: Temporary Tables vs Table Variables in SQL Server
author: PipisCrew
date: 2020-11-09
categories: [sql]
toc: true
---

![](https://i.imgur.com/Tm7x1Qq.png)

Temporary Table (you have to drop)
```js
CREATE TABLE #temp1
(
	date1 smalldatetime,
	username nvarchar(50),
	amount numeric(13,2)
)
```

Temporary table variable (its scope ends when either the batch or the session ends)
```js
DECLARE @product_table TABLE (
    product_name VARCHAR(MAX) NOT NULL,
    brand_id INT NOT NULL,
    list_price DEC(11,2) NOT NULL
)
```

Global temporary table (visible to all sessions (connections), you have to drop)
```js
CREATE TABLE ##tempGlobalB  
(  
	Column1   INT   NOT NULL ,  
	Column2   NVARCHAR(4000)  
);
```

src - https://www.metrostarsystems.com/enterprise-it/temporary-tables-table-variables-sql-server/

> Similar to the temporary table, the table variables do live in the tempdb database, not in the memory.

https://www.sqlservertutorial.net/sql-server-user-defined-functions/sql-server-table-variables/

> Table variables use tempdb similar to how temporary tables use tempdb.

https://sqlperformance.com/2017/04/performance-myths/table-variables-in-memory

more 
https://docs.microsoft.com/en-us/sql/relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization?view=sql-server-ver15

tempDB - https://docs.microsoft.com/en-us/sql/relational-databases/databases/tempdb-database?view=sql-server-ver15

* * *

![](https://i.imgur.com/QzwLEWq.jpg)

> The transaction log for database 'tempdb' is full due to 'ACTIVE_TRANSACTION'

This issue occurs if the size of the tempdb **log file** is not enough to handle tempdb workload, and the **auto growth** of the log file is **set to Off**.

src - https://support.microsoft.com/en-us/help/2963384/kb2963384-fix-sql-server-crashes-when-the-log-file-of-tempdb-database

origin - https://www.pipiscrew.com/?p=19322 temporary-tables-vs-table-variables-in-sql-server