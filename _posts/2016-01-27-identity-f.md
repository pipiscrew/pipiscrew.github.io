---
title: identity field + constraints for a table
author: PipisCrew
date: 2016-01-27
categories: [sql]
toc: true
---

source - [http://stackoverflow.com/a/27523976](http://stackoverflow.com/a/27523976)

SQL Server 

-insert/write into identity field
-disable all constraints for table

```js
--source - http://stackoverflow.com/a/20249170

--disable all constraints for a table
ALTER TABLE Toys NOCHECK CONSTRAINT ALL

--disable all constraints for ALL tables
EXEC sp_msforeachtable "ALTER TABLE ? NOCHECK CONSTRAINT ALL";
```

```js
--disable all constraints for ALL tables
EXEC sp_msforeachtable "ALTER TABLE ? NOCHECK CONSTRAINT ALL";

--delete all from table
delete from [Toys]

--enable to write @ IDENTITY field
SET IDENTITY_INSERT Toys ON
GO

--bulk insert
INSERT INTO [Toys]
	([Toy_ID], [Toy_Language_ID], [Toy_SEO_ID], [Toy_Source])
VALUES 
	(1, 1, 1, ''),
	(2, 2, 1, '');
GO

--re-enable IDENTITY field
SET IDENTITY_INSERT Toys OFF
GO

--enable all constraints
EXEC sp_msforeachtable "ALTER TABLE ? WITH CHECK CHECK CONSTRAINT ALL";
```

origin - http://www.pipiscrew.com/?p=2785 sql-identity-field-constraints-for-a-table