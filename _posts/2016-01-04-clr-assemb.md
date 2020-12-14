---
title: CLR Assemblies in SQL Server
author: PipisCrew
date: 2016-01-04
categories: [sql]
toc: true
---

![snap555](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap555.png)

On SQL 2008 valid TSQL calls are :
```js
CREATE ASSEMBLY [TestAssembly] FROM 0x4D5A90..000

ALTER ASSEMBLY [TestAssembly] FROM 0x4D5A90..000

ALTER ASSEMBLY [TestAssembly] FROM 'C:\TestAssembly.dll'

DROP ASSEMBLY [TestAssembly]

--used to show the installed Assembly.ManifestModule.ModuleVersionId
SELECT ASSEMBLYPROPERTY(N'TestAssembly', 'MvID')
```

### MvID on VStudio

![snap556](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap556.png)

### list the installed assemblies

![snap557](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap557.png)
```js
--https://msdn.microsoft.com/en-us/library/ms131107(v=sql.105).aspx
select * from sys.assembly_files
```

### Refreshing changed .NET SQL CLR assemblies after patching/updates

[http://www.trycatchfinally.net/2013/03/refreshing-changed-net-sql-clr-assemblies-after-patchingupdates/](http://www.trycatchfinally.net/2013/03/refreshing-changed-net-sql-clr-assemblies-after-patchingupdates/)

origin - http://www.pipiscrew.com/?p=3023 clr-assemblies-in-sql-server