---
title: Execute dynamic SQL with parameters
author: PipisCrew
date: 2020-11-10
categories: [sql]
toc: true
---

```js
CREATE OR ALTER PROCEDURE [dbo].[Customers_Mechanism]
(
	@customerId INT,
	@dateCreated datetime
)

DECLARE @tblCust varchar(50),
	@tmpQuery VARCHAR(MAX);

--physical temporary table name
SET @tblCust = CONCAT('tmp_', @mercantId);

--restrict table names to 128 chars
	IF LEN(@tblCust) > 128
	BEGIN
		SET @tblCust = SUBSTRING(@tblCust, 1, 128)
	END

--create table or truncate if exists
	IF EXISTS (SELECT TOP(1) 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'dbo' AND TABLE_NAME = @tblCust)
		BEGIN
			SET @tmpQuery = 'TRUNCATE TABLE ' + @tblCust
		END
	ELSE
		BEGIN
			SET @tmpQuery = 'CREATE TABLE ' + @tblCust + ' (
				[CustomerId] INT NOT NULL,
				[Address] [nvarchar](200) NOT NULL,
				[Telephone] [nvarchar](11) NULL,
				[Amount] [decimal](18, 2) NULL
			)'
		END

--execute SQL string
EXEC(@tmpQuery);

IF @@ERROR <> 0	
	RETURN 0; 

--Dynamic with parameter
SET @tmpQuery = 'INSERT INTO ' + @tblSETS + ' (CustomerId, Address, Telephone, Amount)
				SELECT CustomerId, Address, Telephone, Amount from Customers where dateCreated = @d'

--execute SQL string with param
EXECUTE sp_executesql @tmpQuery, N'@d datetime', @d = @dateCreated

IF @@ERROR <> 0	
	RETURN 0; 
```

multiple parameters as :
```js
-- src - https://stackoverflow.com/a/32516310

EXECUTE sp_executesql @tmpQuery, N'@address nvarchar(200), @telephone nvarchar(11)', 
                              @address = @address, @telephone = @telephone;

```

dealing with XML dynamic param
```js

-- src - https://www.red-gate.com/simple-talk/blogs/using-xml-to-pass-lists-as-parameters-in-sql-server/

DECLARE @sqlCommand nvarchar(1000)
DECLARE @XMLlist XML = '<list>*2**4**6**8**10**15**17**21*</list>'

SET @sqlCommand = 'SELECT x.y.value(''.'',''int'') AS IDs FROM @data.nodes(''/list/i'') AS x ( y )'

EXECUTE sp_executesql @sqlCommand, N'@data XML', @data = @XMLList

```

if you getting the famous 

> Procedure expects parameter '@statement' of type 'ntext/nchar/nvarchar'

make sure you declare the variable as **N**VARCHAR for text, apparently all the datatypes supported.

refs :
https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql
https://www.mssqltips.com/sqlservertip/1160/execute-dynamic-sql-commands-in-sql-server/

origin - https://www.pipiscrew.com/?p=19347 execute-dynamic-sql-with-parameters