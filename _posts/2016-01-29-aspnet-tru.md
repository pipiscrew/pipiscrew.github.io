---
title: o[asp.net] trust levels
author: PipisCrew
date: 2016-01-29
categories: [asp.net]
toc: true
---

source - [http://stackoverflow.com/a/2617483](http://stackoverflow.com/a/2617483)

**Full trust** - your code can do anything that the account running it can do.
**High trust** - same as above except your code cannot call into unmanaged code. i.e. Win32 APIs, COM interop.
**Medium trust** - same as above except your code cannot see any part of the file system except its application directory.
**Low trust** - same as above except your code cannot make any out-of-process calls. i.e. calls to a database, network, etc.
**Minimal trust** - code is restricted from anything but the most trival processing (calculating algorithms).

origin - http://www.pipiscrew.com/?p=3501 asp-net-trust-levels