---
title: String repeat method for C#
author: PipisCrew
date: 2018-07-24
categories: [.net]
toc: true
---

RepeatStringBuilderAppend the best.

```js
//src - https://gunnarpeipman.com/csharp/string-repeat/

static string RepeatForLoop(string s, int n)
{
    var result = s;

    for (var i = 0; i < n - 1; i++)
    {
        result += s;
    }

    return result;
}        

static string RepeatPadLeft(string s, int n)
{
    return "".PadLeft(n, 'X').Replace("X", s);
}

static string RepeatReplace(string s, int n)
{
    return new String('X', n).Replace("X", s);
}

static string RepeatConcat(string s, int n)
{
    return String.Concat(Enumerable.Repeat(s, n));
}

static string RepeatStringBuilderInsert(string s, int n)
{
    return new StringBuilder(s.Length * n)
                .Insert(0, s, n)
                .ToString();
}

static string RepeatStringBuilderAppend(string s, int n)
{
    return new StringBuilder(s.Length * n)
                .AppendJoin(s, new string[n+1])
                .ToString();
}
```

origin - http://www.pipiscrew.com/?p=13846 string-repeat-method-for-c