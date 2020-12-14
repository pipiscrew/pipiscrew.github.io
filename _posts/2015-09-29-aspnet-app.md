---
title: o[asp.net] Application Life Cycle Overview
author: PipisCrew
date: 2015-09-29
categories: [asp.net]
toc: true
---

The main difference in processing stages between IIS 7.0 and IIS 6.0 is in how ASP.NET is integrated with the IIS server. In IIS 6.0, there are two request processing pipelines. One pipeline is for native-code ISAPI filters and extension components. The other pipeline is for managed-code application components such as ASP.NET. In IIS 7.0, the ASP.NET runtime is integrated with the Web server so that there is one unified request processing pipeline for all requests. For ASP.NET developers, the benefits of the integrated pipeline are as follows:

-The integrated pipeline raises all the events that are exposed by the HttpApplication object, which enables existing ASP.NET HTTP modules to work in IIS 7.0 Integrated mode.

-Both native-code and managed-code modules can be configured at the Web server, Web site, or Web application level. This includes the built-in ASP.NET managed-code modules for session state, forms authentication, profiles, and role management. Furthermore, managed-code modules can be enabled or disabled for all requests, regardless of whether the request is for an ASP.NET resource like an .aspx file.

-Managed-code modules can be invoked at any stage in the pipeline. This includes before any server processing occurs for the request, after all server processing has occurred, or anywhere in between.

-You can register and enable or disable modules through an application’s Web.config file.

source [https://msdn.microsoft.com/en-us/library/bb470252.aspx](https://msdn.microsoft.com/en-us/library/bb470252.aspx)

![9](https://www.pipiscrew.com/wp-content/uploads/2015/09/9.jpg)

source - [http://www.codeproject.com/KB/aspnet/ASPDOTNETPageLifecycle.aspx](http://www.codeproject.com/KB/aspnet/ASPDOTNETPageLifecycle.aspx)

origin - http://www.pipiscrew.com/?p=2033 application-life-cycle-overview