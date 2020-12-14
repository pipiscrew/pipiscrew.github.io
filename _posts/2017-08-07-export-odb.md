---
title: Export ODBC
author: PipisCrew
date: 2017-08-07
categories: [news]
toc: true
---

```js

// src - https://gist.github.com/gioxx/e8df26834350c599a0f1

if defined ProgramFiles(x86) (
	echo     Esporto origini dati x86 e x64 ...
	reg export HKLM\SOFTWARE\ODBC\ODBC.INI "C:\ODBC_x86.reg"
	reg export HKLM\SOFTWARE\Wow6432Node\ODBC\ODBC.INI "C:\ODBC_x64.reg"
	reg export HKCU\SOFTWARE\ODBC\ODBC.INI "C:\ODBC_x86_user.reg"
) else (
	echo     Esporto origini dati x86 ...
    reg export HKLM\SOFTWARE\ODBC\ODBC.INI "C:\ODBC_x86.reg"
    reg export HKCU\SOFTWARE\ODBC\ODBC.INI "C:\ODBC_x86_user.reg"
)
```

origin - http://www.pipiscrew.com/?p=9765 export-odbc