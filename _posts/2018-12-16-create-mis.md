---
title: Create missing index on a table on SSMS 2008 and above
author: PipisCrew
date: 2018-12-16
categories: [sql]
toc: true
---

![](https://i.imgur.com/nefSLlx.png)

or

![](https://i.imgur.com/YIlctRL.png)

execute your query
```js
USE AdventureWorks 
GO

SELECT CustomerID, Name, SalesPersonID, ModifiedDate 
FROM Sales.Store 
WHERE (Name='Bike World' AND ModifiedDate > '2004-10-01')
GO
```

If dbase needs an INDEX, will appear this 'Missing Index' green line.

![](https://i.imgur.com/65A7Q8A.png)

Right click > Missing Index Details
![](https://i.imgur.com/9IJuIFY.png)

This will generate T-SQL code for the missing index (SQL Server 2008 Management Studio).
```js
USE [AdventureWorks]
GO

CREATE NONCLUSTERED INDEX []
ON [Sales].[Store] ([Name],[ModifiedDate])

GO
```

name the INDEX name 
```js
CREATE NONCLUSTERED INDEX [IDX_Store_Mod_Date]
```

#create #index #missing

src - [https://www.mssqltips.com/sqlservertip/1945/missing-index-feature-of-sql-server-2008-management-studio/](https://www.mssqltips.com/sqlservertip/1945/missing-index-feature-of-sql-server-2008-management-studio/)

origin - https://www.pipiscrew.com/?p=14499 create-missing-index-on-a-table-on-ssms-2008-and-above