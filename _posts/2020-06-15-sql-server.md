---
title: SQL Server DataReader.GetField return null instead of geography data
author: PipisCrew
date: 2020-06-15
categories: [sql]
toc: true
---

fix **via NuGet** (1.6mb)

Microsoft.SqlServer.Types is a library you can add to your .NET project to work with SQL Server geography and geometry data types in your .NET project.

https://www.nuget.org/packages/Microsoft.SqlServer.Types/

ref - https://stackoverflow.com/q/55466593

<span style="background-color: #ffff00;">NuGet analyzed</span> contains :
-.NET Wrapper (383kb)
-msvcr120.dll (VC++ runtime - 963kb)
-SqlServerSpatial140.dll (native - 732kb)

--

**w/o NuGet**, you can **cast** the field as

```js
SELECT cast(GeoLocation as VARCHAR(max)) FROM table
--or
SELECT cast(GeoLocation as VARBINARY(max)) FROM table
```

origin - https://www.pipiscrew.com/?p=18515 sql-server-datareader-getfield-return-null-instead-of-geography-data