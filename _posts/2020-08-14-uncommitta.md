---
title: Uncommittable transaction is detected at the end of the batch. The transaction is rolled back
author: PipisCrew
date: 2020-08-14
categories: [sql]
toc: true
---

> When the stored procedure throws an error, instead of going in to the catch block I'm getting an exception back saying "Uncommittable transaction is detected at the end of the batch. The transaction is rolled back."
> 
> But if I run the stored procedure in SSMS it works as expected.

To avoid similar situations and implement our logic without problems we can set XACT_ABORT ON in our procedure. When SET XACT_ABORT is ON and T-SQL statement raises a run-time error, SQL Server automatically rolls back the current transaction. By default XACT_ABORT is OFF. 

src - https://www.mssqltips.com/sqlservertip/4018/sql-server-transaction-count-after-execute-indicates-a-mismatching-number-of-begin-and-commit-statements/

not tried yet

<hr>

ref - http://www.sommarskog.se/error_handling/Part2.html

origin - https://www.pipiscrew.com/?p=18902 uncommittable-transaction-is-detected-at-the-end-of-the-batch-the-transaction-is-rolled-back