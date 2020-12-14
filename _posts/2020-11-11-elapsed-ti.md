---
title: Elapsed Time Calculation on SQL Server with dateDiff
author: PipisCrew
date: 2020-11-11
categories: [sql]
toc: true
---

```js
//https://stackoverflow.com/questions/4073340/using-datediff-to-find-duration-in-minutes

DECLARE @t1 DATETIME='2020-11-11 11:28:35'
DECLARE @t2 DATETIME=  GETDATE()
print  CAST(dateDiff(second,@t1,@t2) as INT)

/*
possible values
second
minute
millisecond
*/
```

origin - https://www.pipiscrew.com/?p=19365 elapsed-time-calculation-on-sql-server-with-datediff