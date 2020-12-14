---
title: o[csharp] nullable int to int
author: PipisCrew
date: 2015-12-09
categories: [.net]
toc: true
---

source : [http://stackoverflow.com/a/5995418](http://stackoverflow.com/a/5995418)

```js
v2 = v1 ?? default(int);
```

Also, as of .NET 4.0, Nullable<t> has a "GetValueOrDefault()" method, which is a null-safe getter that basically performs the null-coalescing shown above, so this works too:

```js
v2 = v1.GetValueOrDefault();
```

//traditional
```jsif(v1.HasValue)
   v2=v1.Value
```</t>

origin - http://www.pipiscrew.com/?p=2757 csharp-nullable-int-to-int