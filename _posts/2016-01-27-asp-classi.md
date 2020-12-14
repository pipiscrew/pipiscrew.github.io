---
title: asp classic - IIS - show error on 500 internal error
author: PipisCrew
date: 2016-01-27
categories: [asp_classic]
toc: true
---

###  IIS v6.0 

The error

> An error occurred on the server when processing the URL. Please contact the system administrator.

![snap037](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap037.png)

![snap038](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap038.png)

![snap039](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap039.png)

source - [http://www.reedolsen.com/show-errors-for-classic-asp-pages-in-iis-6/](http://www.reedolsen.com/show-errors-for-classic-asp-pages-in-iis-6/)

###  IIS > v6.0 

The error 

> 500 internal server error

![snap029](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap029.png)

![snap030](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap030.png)

![snap031](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap031.png)

![snap032](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap032.png)

source - [http://serverfault.com/a/671237](http://serverfault.com/a/671237)

#iis6, #iis7

* * *

### asp.net - web.config

[http://stackoverflow.com/a/5385884](http://stackoverflow.com/a/5385884)

**On IIS 6**
```js
//test
<configuration>
    <system.web>
        <customerrors mode="Off"></customerrors>
        <compilation debug="true"></compilation>
    </system.web>
</configuration>
```

**On IIS 7**
```js
//test
<configuration>
    <system.webserver>
        <httperrors errormode="Detailed"></httperrors>
        <asp scripterrorsenttobrowser="true"></asp>
    </system.webserver>
    <system.web>
        <customerrors mode="Off"></customerrors>
        <compilation debug="true"></compilation>
    </system.web>
</configuration>
```

* * *

source - [http://stackoverflow.com/a/30136919/1320686](http://stackoverflow.com/a/30136919/1320686)

> "Unrecognized attribute 'targetFramework'"

In IIS
Click on Application Pools
Right Click on DefaultAppPool --->> Set Application Pool Default....--->>Change .Net Version to V 4.0.

* * *

source - [https://www.inflectra.com/Support/KnowledgeBase/KB5.aspx](https://www.inflectra.com/Support/KnowledgeBase/KB5.aspx)

> Handler "PageHandlerFactory-Integrated" has a bad module "ManagedPipelineHandler" in its module list.

The following steps will usually resolve this issue:

```js
1. Open a command-prompt, and run the following two commands:

C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -i -enable
C:\Windows\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable

2. After this, stop and restart the IIS service.
3. Then try to go to the login page.

```

origin - http://www.pipiscrew.com/?p=3257 asp-classic-show-error-on-500-internal-error