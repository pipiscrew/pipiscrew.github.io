---
title: Dynamic JSON Deserialization
author: PipisCrew
date: 2015-12-11
categories: [.net]
toc: true
---

Read a JSON without need to create a class for deserialization.

Assembly System.Web.Extensions.dll, v4.0.0.0
// C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETFramework\v4.5\System.Web.Extensions.dll

```js
//http://stackoverflow.com/a/6321697

//ask web service
string d = executeRequest(tmp);

//dynamic deserialize the JSON
JavaScriptSerializer js = new JavaScriptSerializer();
dynamic x=js.Deserialize<dynamic>(d);

//access the JSON dynamic fields
Console.WriteLine(x["total"]);
```

### DynamicJson

[https://dynamicjson.codeplex.com/](https://dynamicjson.codeplex.com/)</dynamic>

origin - http://www.pipiscrew.com/?p=2788 net-dynamic-json-deserialization