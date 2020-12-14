---
title: Humanizer
author: PipisCrew
date: 2016-01-31
categories: [.net]
toc: true
---

Meets all your .NET needs for manipulating and displaying strings, enums, dates, times, timespans, numbers and quantities.

[http://humanizr.net/](http://humanizr.net/)

```js
DateTime.UtcNow.AddHours(-30).Humanize() => "yesterday"
DateTime.UtcNow.AddHours(-2).Humanize() => "2 hours ago"

DateTime.UtcNow.AddHours(30).Humanize() => "tomorrow"
DateTime.UtcNow.AddHours(2).Humanize() => "2 hours from now"

DateTimeOffset.AddHours(1).Humanize() => "an hour from now"

// In ar culture
DateTime.UtcNow.AddDays(-1).Humanize() => "أمس"
DateTime.UtcNow.AddDays(-2).Humanize() => "منذ يومين"
DateTime.UtcNow.AddDays(-3).Humanize() => "منذ 3 أيام"
DateTime.UtcNow.AddDays(-11).Humanize() => "منذ 11 يوم"
```

```js
1.ToWords() => "one"
10.ToWords() => "ten"
11.ToWords() => "eleven"
122.ToWords() => "one hundred and twenty-two"
3501.ToWords() => "three thousand five hundred and one"

"dollar".ToQuantity(2, "C0", new CultureInfo("en-US")) => "$2 dollars"
"dollar".ToQuantity(2, "C2", new CultureInfo("en-US")) => "$2.00 dollars"

1.Ordinalize() => "1st"
5.Ordinalize() => "5th"

"some_title".Pascalize() => "SomeTitle"
```

origin - http://www.pipiscrew.com/?p=3526 net-humanizer