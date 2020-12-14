---
title: sql server query date field without hassle
author: PipisCrew
date: 2020-11-05
categories: [sql]
toc: true
---

```js
SELECT * FROM Customers
WHERE CAST(CreatedOn AS DATE) = CAST(GETDATE() AS DATE) --today
--OR
WHERE CAST(CreatedOn AS DATE) = '2020-11-05'
--OR
WHERE CreatedOn BETWEEN '2020-11-05 00:00:00' AND '2020-11-05 23:59:00' 
--OR for yesterday and today
WHERE CAST(CreatedOn AS DATE) >= CAST( dateadd(day, -1, getdate()) AS DATE )
```

origin - https://www.pipiscrew.com/?p=19313 sql-server-query-date-field