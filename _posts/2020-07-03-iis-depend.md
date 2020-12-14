---
title: IIS depends on HTTP windows driver
author: PipisCrew
date: 2020-07-03
categories: [asp.net]
toc: true
---

Lives @ 
```js
//http.sys v10.0.19041.1
//1.531kb on Windows 10x64
//
//http.sys v6.1.7601.17514
//736kb on Windows 7x64
C:\Windows\System32\drivers\http.sys

//registry 'service' settings
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\HTTP
```

so the next time you are in troubles, among iisreset, **first** try restart HTTP driver!!
```js
//once execute this, IIS stopping
net stop http

//start HTTP driver
net start http

//then start IIS
iisreset /start
```

**http.sys** on Windows**7** doesnt have dependencies.
**http.sys** on Windows**10** depends on [MsQuic](https://github.com/microsoft/msquic) (more - [MsQuic, its implementation of Google-spawned TCP-killer QUIC](https://www.theregister.com/2020/05/04/microsoft_reveals_msquic_quic_implementation/))

![](https://i.imgur.com/fPHM8jv.png)

Windows10 http.sys & msquic.sys files, transferred to Windows7 system
![](https://i.imgur.com/3FF62iq.png)

* * *

querying the service with sc
```jssc queryex http```

![](https://i.imgur.com/JMRtyHe.png)

struggling to find out whats wrong, in the end the solution is to stop RedGate.Client.Service.exe

![using Process Hacker - Find Handles](https://i.imgur.com/ZA3kFLn.png)

src - https://forum.red-gate.com/discussion/87115/bug-redgate-client-service-block-http-driver-to-stop

ref
http://woshub.com/killing-windows-services-that-hang-on-stopping/
https://stackoverflow.com/a/38350818

* * *

moreover (an old thread) :

> Services MMC doesn't list http, as it's a driver and not exactly a service.

This command will tell you, how **http driver** is configured and what happens whey they start. From Admin Command Prompt, type:

```jssc qc http```

Thanks to Win32Guy and Jacques Koekemoer for the wonderful work, interpretation & Technet link. SC : Microsoft Docs

I want to take into account the broader aspects, keep Print Spooler in the center & develop an understanding. I want to mention:

**Print Spooler Dependency Tree**, i.e., The system components Print Spooler depends upon:

>>Print Spooler (Spooler) depends on Remote Procedure Call (RPCSS) & HTTP Service (HTTP)
>>RPCSS depends on DCOM Server Process Launcher (DcomLaunch) & RPC Endpoint Mapper (RpcEptMapper)
>>HTTP doesn't have any dependencies.
>>Dcomlaunch & RpcEptMapper doesn't have any dependencies.

So now we have found the proper tree & roots. We have to start with the roots!
HTTP is a service & a driver, but all the others are services & are located in/by services.msc. You can't find HTTP there.
A question arises, how to work with/on HTTP? **sc** commands are good to work with HTTP as well as services mentioned in services.msc.

src - https://superuser.com/a/1059096

origin - https://www.pipiscrew.com/?p=18556 iis-depends-on-http-windows-driver