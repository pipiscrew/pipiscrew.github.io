---
title: o[c#] Connecting to Oracle Database
author: PipisCrew
date: 2016-10-28
categories: [.net]
toc: true
---

fixes :
The provider is not compatible with the version of Oracle client
OCIEnvCreate failed with return code -1 but error message text was not available.

1- goto http://www.oracle.com/technetwork/topics/dotnet/downloads/index.html

click

> 32-bit ODAC Xcopy and NuGet Downloads

one the next screen **accept**
at the 3rd section "ODAC 12c Release 4 (12.1.0.2.4)" click the 

> ODAC121024Xcopy_32bit.zip 69.2 MB (72,617,613 bytes)

registration required. btw I collect all the [needed files](https://www.mediafire.com/?qr1z4xlop17wl58).

2-extract the downloaded file **ODAC121024Xcopy_32bit.zip**. We will use only the following folders
instantclient_12_1
odp.net4
oramts

copy from **instantclient_12_1** to your PRJ bin :
oci.dll
orannzsbb12.dll
oraocci12.dll
oraocci12d.dll
oraociei12.dll
oraons.dll

copy from **odp.net4/odp.net/bin/4** to your PRJ bin :
Oracle.DataAccess.dll

copy from **odp.net4/bin** to your PRJ bin :
OraOps12.dll

copy from **oramts/bin** to your PRJ bin :
oramts.dll
oramts12.dll
oramtsus.dll

3-at your VS PRJ properties select > Build for x86 (default is AnyCPU)

4-add reference to PRJ/bin/Oracle.DataAccess.dll

```js
//example of connection
string connString = "Data Source=(DESCRIPTION =(ADDRESS = (PROTOCOL = TCP)(HOST = "
	 + host + ")(PORT = " + port + "))(CONNECT_DATA = (SERVER = DEDICATED)(SERVICE_NAME = "
	 + sid + ")));Password=" + password + ";User ID=" + user;

OracleConnection conn = new OracleConnection();

conn.ConnectionString = connString;
```

<del datetime="2016-10-28T17:28:41+00:00">Old way is to use the System.Data.OracleClient.dll</del>
New way is to use the Oracle.DataAccess.dll

source - http://o7planning.org/en/10509/connecting-to-oracle-database-using-csharp-without-oracle-client

origin - http://www.pipiscrew.com/?p=6204 c-connecting-to-oracle-database