---
title: Try..Catch inside Procedure (SP)
author: PipisCrew
date: 2020-11-11
categories: [sql]
toc: true
---

```js
BEGIN TRY
--your code here
END TRY  
BEGIN CATCH  
	INSERT INTO [dbo].[myErrorLog] ([Description], [daterec]) 
	VALUES (CAST(ERROR_MESSAGE() AS VARCHAR(500)), GETDATE())   
END CATCH; 
```

inside **BEGIN/END CATCH** we can gather the following information
ERROR_NUMBER() returns the number of the error.
ERROR_SEVERITY() returns the severity.
ERROR_STATE() returns the error state number.
ERROR_PROCEDURE() returns the name of the stored procedure or trigger where the error occurred.
ERROR_LINE() returns the line number inside the routine that caused the error.
ERROR_MESSAGE() returns the complete text of the error message. The text includes the values supplied for any substitutable parameters, such as lengths, object names, or times.

ref
https://docs.microsoft.com/en-us/sql/t-sql/language-elements/try-catch-transact-sql?view=sql-server-ver15
https://www.sqlservertutorial.net/sql-server-stored-procedures/sql-server-try-catch/

origin - https://www.pipiscrew.com/?p=19367 try-catch-inside-procedure-sp