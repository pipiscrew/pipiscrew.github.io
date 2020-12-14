---
title: MySQL count filesize of database
author: PipisCrew
date: 2020-08-29
categories: [sql]
toc: true
---

//https://www.a2hosting.com/kb/developer-corner/mysql/determining-the-size-of-mysql-databases-and-tables

```js
//whole dbase
SELECT table_schema AS "Database", 
ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS "Size (MB)" 
FROM information_schema.TABLES 
GROUP BY table_schema;

//specific catalog
SELECT table_name AS "Table",
ROUND(((data_length + index_length) / 1024 / 1024), 2) AS "Size (MB)"
FROM information_schema.TABLES
WHERE table_schema = "database_name"
ORDER BY (data_length + index_length) DESC;
```

origin - https://www.pipiscrew.com/?p=18990 mysql-count-filesize-of-database