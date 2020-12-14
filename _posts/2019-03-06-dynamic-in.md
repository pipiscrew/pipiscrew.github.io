---
title: Dynamic in C# 4.0- Introducing the ExpandoObject
author: PipisCrew
date: 2019-03-06
categories: [.net]
toc: true
---

[https://devblogs.microsoft.com/csharpfaq/dynamic-in-c-4-0-introducing-the-expandoobject/](https://devblogs.microsoft.com/csharpfaq/dynamic-in-c-4-0-introducing-the-expandoobject/)

* * *

**Reflection comparison**
[https://www.red-gate.com/simple-talk/dotnet/.net-framework/a-defense-of-reflection-in-.net/](https://www.red-gate.com/simple-talk/dotnet/.net-framework/a-defense-of-reflection-in-.net/)

* * *

You can use **KORM**. Object relation mapper, which has provider for MsAccess Kros.KORM.MsAccess. KORM allow materialize ADO.NET classies like DbReader to IEnumerable. For example database.ModelBuilder.Materialize(reader)
https://www.nuget.org/packages/Kros.KORM.MsAccess/

* * *

**Convert ExpandoObject to DataTable**
[http://www.fruitbatscode.com/net/c/convert-expandoobject-to-datatable](http://www.fruitbatscode.com/net/c/convert-expandoobject-to-datatable)

* * *

<span style="background-color: #ffff00;">**Adding properties and methods to an ExpandoObject, dynamically!**</span>
https://www.filipekberg.se/2011/10/02/adding-properties-and-methods-to-an-expandoobject-dynamicly/

A **typical dynamic** setup that creates a **dynamic object** and adds a static amount of properties might look like this:

```js
//src filipekberg
dynamic person = new ExpandoObject();
person.Name = "Filip";
person.Age = 24;```

What is interesting about the ExpandoObject is that it implements the interface: ]IDictionary<string, object="">

So what this means is that if we cast the person-object to an **IDictionary** we will be able to do some really cool stuff with it. The same code above but re-written to make use of the **dictionary** instead could look like this:

```js
dynamic person = new ExpandoObject();
var dictionary = (IDictionary<string, object="">)person;

dictionary.Add("Name", "Filip");
dictionary.Add("Age", 24);```</string,></string,>

origin - https://www.pipiscrew.com/?p=14734 dynamic-in-c-4-0-introducing-the-expandoobject