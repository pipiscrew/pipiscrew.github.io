---
title: convert date.month to text
author: PipisCrew
date: 2016-02-22
categories: [sql]
toc: true
---

references :
[https://msdn.microsoft.com/en-us/library/ms174398(v=sql.105).aspx](https://msdn.microsoft.com/en-us/library/ms174398(v=sql.105).aspx)
[http://stackoverflow.com/questions/185520/convert-month-number-to-month-name-function-in-sql](http://stackoverflow.com/questions/185520/convert-month-number-to-month-name-function-in-sql)

```js
--Specifies the language environment for the session. The session language determines the datetime formats and system messages.
SET LANGUAGE Greek;

--full month text
SELECT DATENAME(month, Last_Updated) from Customers

--way 1 short month text
SELECT CONVERT(CHAR(3), DATENAME(MONTH, Last_Updated)) from Customers

--way 2 short month text
SELECT CAST(Last_Updated AS CHAR(3)) from Customers
```

origin - http://www.pipiscrew.com/?p=3936 sql-convert-date-month-to-text