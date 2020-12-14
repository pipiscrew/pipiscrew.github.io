---
title: desktop application - callback from WCF
author: PipisCrew
date: 2016-01-25
categories: [.net,asp.net]
toc: true
---

### Default Timeout - Binding.ReceiveTimeout Property

The default is 10 minutes, so you always have to increase both of them to make a difference when using a reliable session.
stackoverflow - http://stackoverflow.com/questions/3037734/default-timeout-values-for-wcf-endpoints
microsoft url - [https://msdn.microsoft.com/en-us/library/system.servicemodel.channels.binding.receivetimeout.aspx](https://msdn.microsoft.com/en-us/library/system.servicemodel.channels.binding.receivetimeout.aspx)

### Duplex Services

In WCF, there are some other techniques like Duplex Services to solve this.
https://msdn.microsoft.com/en-us/library/ms731064(v=vs.90).aspx

references :
http://stackoverflow.com/questions/19705804/implementing-a-web-service-callback
http://stackoverflow.com/questions/5739501/how-can-a-wcf-service-raise-events-to-its-clients

origin - http://www.pipiscrew.com/?p=3387 net-desktop-application-callback-from-wcf