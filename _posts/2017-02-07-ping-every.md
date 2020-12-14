---
title: Ping every X minutes
author: PipisCrew
date: 2017-02-07
categories: [app]
toc: true
---

http://superuser.com/questions/345214/how-can-i-perform-a-ping-every-x-minutes-and-check-the-response-time

```js
@ECHO OFF
set IPADDRESS=x.x.x.x
set INTERVAL=10
:PINGINTERVAL
ping google.com -n 1
timeout %INTERVAL%
GOTO PINGINTERVAL
```

or

```js
ping -i 30 8.8.8.8
ping -t google.com -w 10000

ping google.com -n 1
```

http://www.nirsoft.net/utils/multiple_ping_tool.html

#ping

origin - http://www.pipiscrew.com/?p=6661 ping-every-x-minutes