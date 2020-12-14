---
title: ISNULL with NULLIF to avoid empty string
author: PipisCrew
date: 2020-06-09
categories: [sql]
toc: true
---

```js
--general function if null then ''
ISNULL(the_field, '')

--with NULLIF check for empty field
ISNULL(NULLIF(the_field,''), '')

--select all records that is not null or empty
SELECT TOP 100 * FROM table WHERE  ISNULL(NULLIF(the_field,'' ),NULL) IS NOT NULL ORDER BY 1 DESC   

--Comparing NULLIF and CASE

USE AdventureWorks2008R2;
GO
SELECT ProductID, MakeFlag, FinishedGoodsFlag, 
   NULLIF(MakeFlag,FinishedGoodsFlag)AS 'Null if Equal'
FROM Production.Product
WHERE ProductID < 10;
GO

SELECT ProductID, MakeFlag, FinishedGoodsFlag,'Null if Equal' =
   CASE
       WHEN MakeFlag = FinishedGoodsFlag THEN NULL
       ELSE MakeFlag
   END
FROM Production.Product
WHERE ProductID < 10;
GO
```

src - https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms177562(v=sql.105)

origin - https://www.pipiscrew.com/?p=18456 isnull-with-nullif-to-avoid-empty-string