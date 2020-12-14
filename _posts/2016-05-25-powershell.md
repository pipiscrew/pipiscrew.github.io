---
title: PowerShell – Querying SQL Server
author: PipisCrew
date: 2016-05-25
categories: [news,sql]
toc: true
---

[http://blog.sqlauthority.com/2016/05/24/powershell-querying-sql-server-command-line/](http://blog.sqlauthority.com/2016/05/24/powershell-querying-sql-server-command-line/)

```js
Invoke-SqlCmd -Query "Select * from sys.databases" -ServerInstance "."
```

origin - http://www.pipiscrew.com/?p=5627 powershell-querying-sql-server