---
title: Performance Timer Logging
author: PipisCrew
date: 2015-12-21
categories: [.net]
toc: true
---

```js
var timer = Stopwatch.StartNew();
var ms = timer.ElapsedMilliseconds;

Just 2 Lines and no ugly indenting of my code. There is really no need to stop the Stopwatch. No resources will be freed if you do, it just stops counting.
```

```js
using System.Diagnostics;

var timer = new Stopwatch();
timer.Start();

// do something you want to profile

timer.Stop();
var ms = timer.ElapsedMilliseconds;

// write timing to logs
```

First, here's the usage example of the performance timing logging class that will be listed below:

```js
using (new PerfTimerLogger("name of code being profiled"))
{
    // do something you want to profile
}
```
Now, as you can see the above code is MUCH simpler to implement within your code and not very intrusive. Basically, 2 lines of code, instead of 4; and not extra variables to keep track of.

Here's an implementation of the PerfTimerLogger class that allows it to be used as the above example demonstrates:
```js
using System.Diagnostics;

public class PerfTimerLogger : IDisposable
{
    public PerfTimerLogger(string message)
    {
        this._message = message;
        this._timer = new Stopwatch();
        this._timer.Start();
    }

    string _message;
    Stopwatch _timer;

    public void Dispose()
    {
        this._timer.Stop();
        var ms = this._timer.ElapsedMilliseconds;

        // log the performance timing with the Logging library of your choice
        // Example:
        // Logger.Write(
        //     string.Format("{0} - Elapsed Milliseconds: {1}", this._message, ms)
        // );
    }
}
```

origin - http://www.pipiscrew.com/?p=2875 net-performance-timer-logging