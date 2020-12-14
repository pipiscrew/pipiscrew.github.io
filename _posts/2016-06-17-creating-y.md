---
title: Creating Your Own Custom Dynamic C# Classes
author: PipisCrew
date: 2016-06-17
categories: [.net]
toc: true
---

the class:

```js
//source - http://dontcodetired.com/blog/post/Creating-Your-Own-Custom-Dynamic-C-Classes
using System.Collections.Generic;
using System.Dynamic;
using System.Text;

namespace CustomDynamic
{
    class MyDynamicClass : DynamicObject
    {
        private readonly Dictionary<string, object> _dynamicProperties = new Dictionary<string, object>(); 

        public override bool TrySetMember(SetMemberBinder binder, object value)
        {
            _dynamicProperties.Add(binder.Name, value);

            // additional error checking code omitted

            return true;
        }

        public override bool TryGetMember(GetMemberBinder binder, out object result)
        {
            return _dynamicProperties.TryGetValue(binder.Name, out result);
        }

        public override string ToString()
        {
            var sb = new StringBuilder();

            foreach (var property in _dynamicProperties)
            {
                sb.AppendLine($"Property '{property.Key}' = '{property.Value}'");
            }

            return sb.ToString();
        }
    }
}
```

use of :
```js
//source - http://dontcodetired.com/blog/post/Creating-Your-Own-Custom-Dynamic-C-Classes
using System;

namespace CustomDynamic
{
    class Program
    {
        static void Main(string[] args)
        {            
            dynamic d = new MyDynamicClass();

            // Need to declare as dynamic, the following cause compilation errors:
            //      MyDynamicClass d = new MyDynamicClass();
            //      var d = new MyDynamicClass();

            // Dynamically add properties
            d.Name = "Sarah"; // TrySetMember called with binder.Name of "Name"
            d.Age = 42; // TrySetMember called with binder.Name of "Age"

            Console.WriteLine(d.Name); // TryGetMember called
            Console.WriteLine(d.Age); // TryGetMember called

            Console.ReadLine();
        }
    }
}
```

origin - http://www.pipiscrew.com/?p=5842 creating-your-own-custom-dynamic-c-classes