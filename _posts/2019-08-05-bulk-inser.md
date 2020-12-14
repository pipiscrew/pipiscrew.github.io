---
title: Bulk Insert Data into SQL Server to SQL Server 2017+AZURE
author: PipisCrew
date: 2019-08-05
categories: [sql]
toc: true
---

Imports a data file into a database table or view in a user-specified format in SQL Server. **SQL Server 2017** provides the BULK INSERT statement to perform large imports of data into SQL Server using T-SQL.

```js
--src - https://www.mssqltips.com/sqlservertip/6109/bulk-insert-data-into-sql-server/

BULK INSERT Sales
FROM 'C:\temp\1500000 Sales Records.csv'
WITH (FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR='\n',
    BATCHSIZE=250000);
```

ref - https://docs.microsoft.com/en-us/sql/t-sql/statements/bulk-insert-transact-sql?view=sql-server-2017

origin - https://www.pipiscrew.com/?p=15171 bulk-insert-data-into-sql-server-to-sql-server-2017azure