---
title: Windows Automation API- UI Automation on VS2012
author: PipisCrew
date: 2017-07-10
categories: [.net]
toc: true
---

http://imgur.com/a/PxM4E

```js
//found the dll
//C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\ReferenceAssemblies\v4.0\
//C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\

using Microsoft.VisualStudio.TestTools.UITesting;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace CodedUITestProject1
{
    class Program
    {
        static void Main()
        {
            // You need to call Playback.Initialize() before you execute
            // the coded UI part, and then Playback.Cleanup() after.
            //https://stackoverflow.com/a/17683759/1320686
            Playback.Initialize();

            CodedUITest1 el = new CodedUITest1();

            el.CodedUITestMethod1();

            Playback.Cleanup();
        }

    }
}
```

#macro #WM_GETTEXT

origin - http://www.pipiscrew.com/?p=9011 windows-automation-api-ui-automation-on-vs2012