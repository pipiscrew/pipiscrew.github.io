---
title: DAX functions in SQL Server 2016
author: PipisCrew
date: 2016-01-04
categories: [sql]
toc: true
---

This new function returns a column with the consecutive dates from a start date until a specified end date. The following example will show all the days between January 1, 2015 and January 31, 2015.

```js
evaluate
(
CALENDAR (DATE (2015, 1, 1), DATE (2015, 1, 31))
)```

[https://www.mssqltips.com/sqlservertip/4130/new-dax-functions-in-sql-server-2016/](https://www.mssqltips.com/sqlservertip/4130/new-dax-functions-in-sql-server-2016/)

origin - http://www.pipiscrew.com/?p=3065 sql-dax-functions-in-sql-server-2016