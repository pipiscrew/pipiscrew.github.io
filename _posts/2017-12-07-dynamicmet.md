---
title: DynamicMethod
author: PipisCrew
date: 2017-12-07
categories: [.net]
toc: true
---

> Given sufficient security permissions, they allow code to skip just-in-time (JIT) visibility checks and access the private and protected data of objects.

```js
//https://stackoverflow.com/a/6364868
delegate void foo();

public static void show(string foo)
{
    MessageBox.Show(foo);
}

public void test()
{
    DynamicMethod dm = new DynamicMethod("foo", null, null);
    ILGenerator gen = dm.GetILGenerator();
    gen.Emit(OpCodes.Ldstr, "hello world");
    gen.EmitCall(OpCodes.Call, this.GetType().GetMethod("show"),null);
    gen.Emit(OpCodes.Ret);
    var b = dm.CreateDelegate(typeof(foo)) as foo;
    b();
}
```

https://www.filipekberg.se/2011/10/11/creating-static-methods-at-runtime/
https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/how-to-define-and-execute-dynamic-methods

https://www.codeproject.com/Articles/15845/A-class-to-dynamically-create-delegates-of-functio
https://github.com/IDisposable/Dynamic

https://www.codeproject.com/Articles/531028/Encrypted-code-compiled-at-runtime
http://www.castleproject.org/projects/dynamicproxy/

Libs :
https://github.com/kevin-montrose/Sigil
https://github.com/skbkontur/gremit

origin - http://www.pipiscrew.com/?p=11560 dynamicmethod