---
title: MiniToolBox
author: PipisCrew
date: 2015-11-27
categories: [app]
toc: true
---

## System Log

download 

[http://www.bleepingcomputer.com/download/minitoolbox/](http://www.bleepingcomputer.com/download/minitoolbox/)

Check the following checkboxes:
-List last 10 Event Viewer log
-List Installed Programs
-List Users, Partitions and Memory size.

* * *

## Get system information

[http://www.piriform.com/speccy](http://www.piriform.com/speccy)

[download](http://www.softpedia.com/get/PORTABLE-SOFTWARE/System/System-Info/Speccy-Portable.shtml)

* * *

## Clear Windows Log

Paste it to a bat file, run it as administrator!
source - [http://winaero.com/blog/how-to-clear-the-windows-event-log-from-the-command-line/](http://winaero.com/blog/how-to-clear-the-windows-event-log-from-the-command-line/)

```js
@echo off
FOR /F "tokens=1,2*" %%V IN ('bcdedit') DO SET adminTest=%%V
IF (%adminTest%)==(Access) goto noAdmin
for /F "tokens=*" %%G in ('wevtutil.exe el') DO (call :do_clear "%%G")
echo.
echo Event Logs have been cleared!
goto theEnd
:do_clear
echo clearing %1
wevtutil.exe cl %1
goto :eof
:noAdmin
echo You must run this script as an Administrator!
echo.
:theEnd
```

origin - http://www.pipiscrew.com/?p=2511 app-minitoolbox