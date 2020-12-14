---
title: Remove trailing zeros from decimal in SQL Server
author: PipisCrew
date: 2020-10-16
categories: [sql]
toc: true
---

```js
-- src    - https://stackoverflow.com/a/18520357
-- ms doc - https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings
SELECT FORMAT(CAST(2.33000       AS DECIMAL(9,6)), 'g15')  -- '2.33'
```

origin - https://www.pipiscrew.com/?p=19223 remove-trailing-zeros-from-decimal-in-sql-server