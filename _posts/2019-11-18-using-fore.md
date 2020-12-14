---
title: Using foreach with index in C#
author: PipisCrew
date: 2019-11-18
categories: [.net]
toc: true
---

```js
// foreach with a "manual" index
int index = 0;
foreach (var item in collection)
{
    DoSomething(item, index);
    index++;
}

// normal for loop
for (int index = 0; index < collection.Count; index++)
{
    var item = collection[index];
    DoSomething(item, index);
}

foreach (var (item, index) in collection.WithIndex())
{
    DoSomething(item, index);
}
```

ref - https://thomaslevesque.com/2019/11/18/using-foreach-with-index-in-c/

origin - https://www.pipiscrew.com/?p=15811 using-foreach-with-index-in-c