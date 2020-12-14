---
title: SSL Security Error for Microsoft SQL Driver
author: PipisCrew
date: 2020-05-25
categories: [sql]
toc: true
---

We commonly see the following error from customers that migrate to us from providers that use an older SQL driver:

> [Microsoft][ODBC SQL Server Driver][DBNETLIB]SSL Security error
> 
> or
> 
> TCP Provider: An existing connection was forcibly closed by the remote host

solution :

use 
```js
Driver={SQL Server Native Client 11.0}
or
Driver={ODBC Driver 17 for SQL Server}
```

src - https://community.hostek.com/t/ssl-security-error-for-microsoft-sql-driver/348

origin - https://www.pipiscrew.com/?p=18411 ssl-security-error-for-microsoft-sql-driver