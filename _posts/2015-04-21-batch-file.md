---
title: Batch file For Each..Do
author: PipisCrew
date: 2015-04-21
categories: []
toc: true
---

```js
FOR /D %%X IN (C:\Windows\assembly\NativeImages_*) DO echo %%X
pause
```

advanced use 

```js
@echo off
FOR /D %%X IN (C:\Windows\assembly\NativeImages_*) DO call :letloop %%X
GOTO :EOF

:letloop
rmdir /S /Q "%1\YourDirectory Here"
echo Done
GOTO :EOF
```

origin - http://www.pipiscrew.com/?p=2897 app-batch-file-for-each-do