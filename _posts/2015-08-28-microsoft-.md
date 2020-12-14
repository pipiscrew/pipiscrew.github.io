---
title: Microsoft Starts Collecting User Data from Windows 7 and Windows 8 PCs
author: PipisCrew
date: 2015-08-28
categories: [news]
toc: true
---

reference
[http://news.softpedia.com/news/microsoft-starts-collecting-user-data-from-windows-7-and-windows-8-pcs-490302.shtml](http://news.softpedia.com/news/microsoft-starts-collecting-user-data-from-windows-7-and-windows-8-pcs-490302.shtml)
[http://forums.mydigitallife.info/threads/24902-Windows-Loader-Support-and-chat/page2107?p=1124797](http://forums.mydigitallife.info/threads/24902-Windows-Loader-Support-and-chat/page2107?p=1124797)

> http://superuser.com/a/166255
> It's another syntax: xxx.xxx.xxx.xxx somedomain.com
> 
> Some examples to explain it:
> 
> 127.0.0.1 .com this line will block all outgoing dnsrequests ending with .com
> 127.0.0.1 somesite.com will block all outgoing dnsrequests ending with somesite.com
> 12.2.3.1 www.dns.com will lead all outgoing dnsrequests ending with www.dns.com to 12.2.3.1
> You block/lead all second (third,fourth...) level urls with the top(second,third...) level url in the hosts file.

> http://www.angelfire.com/comics2/fatboy9175/
> the list - http://www.angelfire.com/comics2/fatboy9175/MShosts.txt
> 
> # NOTE: In WinXP SP2 or later, adding these lines to the HOSTS file won't be fully effective thanks to
> # Micro$haft's hidden rules in the "dnsapi.dll" file which override manual settings for certain M$-related
> # domains. To completely block Microsoft out of your system, you will have to add these to a third party
> # firewall, or hack dnsapi.dll, which I wouldn't advise unless you know what you're doing. You can open the
> # dll file with notepad or a hex editor to see all the domains included in Windows' hidden whitelist.
> # I recommend Acrylic DNS Proxy. It has its own hosts file that also supports wildcard rules, so instead
> # of needing thousands of entries that end in microsoft.com, you can just add *.microsoft.com and kill em all.

<strong stlye="color:red">Acrylic DNS Proxy-**  [http://mayakron.altervista.org/wikibase/show.php?id=AcrylicHome](http://mayakron.altervista.org/wikibase/show.php?id=AcrylicHome)</strong>

origin - http://www.pipiscrew.com/?p=1732 microsoft-starts-collecting-user-data-from-windows-7-and-windows-8-pcs