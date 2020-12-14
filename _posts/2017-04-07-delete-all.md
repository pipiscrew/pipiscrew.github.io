---
title: Delete all folders and subfolders with DOS command is faster than windows
author: PipisCrew
date: 2017-04-07
categories: [dos]
toc: true
---

paste&save to x.bat

```js
for /f "tokens=*" %%G in ('dir /AD /B') do del /f/s/q "%%G" > nul && rd "%%G" /s /q
```

tested&working on network path.

src - http://stackoverflow.com/a/6208144/1320686

origin - http://www.pipiscrew.com/?p=7535 delete-all-folders-and-subfolders-with-dos-command-is-faster-than-windows