---
title: o[vs.net] Diff Tool for local files
author: PipisCrew
date: 2016-01-04
categories: [.net]
toc: true
---

In the tools directory of Visual Studio (C:\Program Files (X86)\Microsoft Visual Studio 11.0 (or 12.0)\Common\IDE\ you find the tool VsDiffMerge.exe
Tip: You can also use %VS110COMNTOOLS% on the commandline to point to this directory.

When you start VSDiffMerge, the diff / merge tool starts up with two files that you choose.

```js
%VS110COMNTOOLS%
one dir back, enter to IDE, execute :
vsdiffmerge.exe "File1" "File2"
```

source [http://roadtoalm.com/2013/10/22/use-visual-studio-as-your-diff-and-merging-tool-for-local-files/](http://roadtoalm.com/2013/10/22/use-visual-studio-as-your-diff-and-merging-tool-for-local-files/)

use with GIT - [https://github.com/Inmeta/Knowledge/wiki/Setting-Up-DiffMerge](https://github.com/Inmeta/Knowledge/wiki/Setting-Up-DiffMerge)

* * *

vsdiff.cmd - so, now drag&drop two files from explorer to vsdiff.cmd
```js
"%VS110COMNTOOLS%/../IDE/vsdiffmerge.exe" "%1" "%2"
```

similar article - [http://elbruno.com/2015/12/22/vs2015-compare-2-external-files-in-visual-studio-from-the-ide/](http://elbruno.com/2015/12/22/vs2015-compare-2-external-files-in-visual-studio-from-the-ide/)

origin - http://www.pipiscrew.com/?p=2302 vs-net-diff-tool-for-local-files