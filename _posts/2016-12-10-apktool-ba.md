---
title: apktool basics
author: PipisCrew
date: 2016-12-10
categories: [android,news]
toc: true
---

> Exception in thread "main" brut.androlib.AndrolibException: Could not decode arsc file

solution :
```js
//src - http://stackoverflow.com/a/30695269/1320686
//goto to command line and execute :
apktool.jar if framework-res.apk
```

* * *

for decompile use (will create a folder x near apktool) :
```js
apktool.jar d "c:\test\app_name.apk"
```

for compile use (will create a dist folder inside c:\test\) :
```js
apktool.jar b "app_name"
```

src - http://forum.xda-developers.com/showthread.php?t=2213985

#apktool

origin - http://www.pipiscrew.com/?p=6361 apktool-basics