---
title: Oracle DSN and tnsnames
author: PipisCrew
date: 2018-10-09
categories: [sql]
toc: true
---

Depend on the software we would like to use the DSN, we choosing accordingly 32 or 64bit. Go to Control Panel > Admin Tools > ODBC Data sources (32bit).

The applications, seeking for DSN they looking always the **System DSN** tab. Once you press add and choose **Oracle in OraClient** the **Oracle ODBC Driver Configuration** form will appear.

The only way to configure a connection that doesnt use the default port (1521) is through **DSN** via **TNS Service Name** combo.

By default when installing [ORACLE CLIENT](https://www.oracle.com/technetwork/topics/dotnet/downloads/index.html), creates the **ORACLE_HOME** and **TNS_ADMIN** environment variables (aka Control Panel > System > Advanced System Settings > Environment variables button)

Afterall, by going to a **windows explorer window** and typing **%TNS_ADMIN%** and pressing enter, you landing to a folder that **tnsnames.ora** exists, if not create it!

example :

```js
xxxsid2.domain.com = 
 (DESCRIPTION = 
  (ADDRESS_LIST = 
   (ADDRESS = (PROTOCOL = TCP) (HOST = server.domain.com) (PORT = 1556))
    )
    (CONNECT_DATA = 
     (SID = xxxsid2)
    )
   )

xxxsid.domain.com = 
 (DESCRIPTION = 
  (ADDRESS_LIST = 
   (ADDRESS = (PROTOCOL = TCP) (HOST = server.domain.com) (PORT = 1554))
    )
    (CONNECT_DATA = 
     (SID = xxxsid)
    )
   )
```

once we alter the file as we like, need to reload the **Oracle ODBC Driver Configuration** form, now we can choose via **TNS Service Name** combo the connection ALIAS (ex. xxxsid.domain.com).

[PDF with pictures](https://docdroid.net/nrRxwu3)

ref - http://www.interfaceware.com/manual/odbc_oracle.html
ref - https://www.oracle.com/technetwork/database/features/oci/ic-faq-094177.html
ORAClient - https://www.oracle.com/technetwork/topics/dotnet/downloads/index.html
> Choose “xcopy, NuGet” > 32-bit ODAC 12.1.0.2.4 - 72,617,613 bytes - October 5, 2015
[Microsoft.Power Query for Excel](https://www.microsoft.com/en-us/download/details.aspx?id=39379)

origin - https://www.pipiscrew.com/?p=14340 oracle-dsn-and-tnsnames