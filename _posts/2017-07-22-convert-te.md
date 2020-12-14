---
title: Convert text files to UTF-8
author: PipisCrew
date: 2017-07-22
categories: [.net]
toc: true
---

It provides a very simple interface to let you convert all text files to UTF-8 encoding

[http://www.rotatingscrew.com/utfcast-express.aspx](http://www.rotatingscrew.com/utfcast-express.aspx)

**Steven Wittens** (aka unconed) declaration :

> The UTF-8 BOM was a Microsoft invention. Nobody else uses it, and it breaks tons of things. Two examples off the top of my head: Unix hashbang scripts (i.e. #!/bin/bash), and PHP scripts (the BOM will trigger HTTP header finalization before any code is run).

use the following to write files w/o BOM : 
```js
//http://stackoverflow.com/a/2503049
//https://msdn.microsoft.com/en-us/library/s064f8w2(v=vs.110).aspx

Encoding utf8WithoutBom = new UTF8Encoding(false);
```

origin - http://www.pipiscrew.com/?p=1394 convert-text-files-to-utf-8