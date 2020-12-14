---
title: BEGIN TRAN, ROLLBACK TRAN, and COMMIT TRAN
author: PipisCrew
date: 2019-03-01
categories: [sql]
toc: true
---

Since we specified a BEGIN TRAN, the transaction is now waiting on a ROLLBACK or COMMIT. 

While the transaction is waiting it has created a lock on the table and any other processes that are trying to access TABLE are now being blocked. Be careful using BEGIN TRAN and make sure you immediately issue a ROLLBACK or COMMIT!

BEGIN TRAN
update TABLE set field = 'cat' where istime = 1

ROLLBACK TRAN
COMMIT TRAN

src - https://www.mssqltips.com/sqlservertutorial/3305/what-does-begin-tran-rollback-tran-and-commit-tran-mean/

origin - https://www.pipiscrew.com/2019/03/begin-tran-rollback-tran-and-commit-tran/ begin-tran-rollback-tran-and-commit-tran