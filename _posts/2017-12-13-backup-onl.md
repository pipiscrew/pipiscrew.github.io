---
title: Backup only the source files from an Android studio project
author: PipisCrew
date: 2017-12-13
categories: [android]
toc: true
---

A quick method via batch file to backup your valuable source files only, from a gradle project. Paste it to a batch file inside your project folder and execute it, the archive will created (excluding the unwanted files) one dir back.

<center>![alt](https://i.imgur.com/laI7bjq.png)</center>

```js
@echo off
REM get current folder name
for %%a in (.) do set currentfolder=%%~na
REM echo %currentfolder%

REM maybe here need an adjustment due your system locale settings
set YYYYMMDD=%DATE:~10,4%%DATE:~7,2%%DATE:~4,2%_%time:~0,2%%time:~3,2%%time:~6,2%

cd /d %ProgramFiles(x86)%\WinRAR\
rar.exe a -ep1 -r "%~dp0..\%currentfolder%%YYYYMMDD%" -x*.jar -x*.aar -x*\build -x*\.gradle -x*\.idea "%~dp0"

pause
```

origin - http://www.pipiscrew.com/?p=11580 backup-only-the-source-files-from-an-android-studio-project