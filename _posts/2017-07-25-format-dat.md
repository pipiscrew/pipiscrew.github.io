---
title: Format Date or Datetime to Excel 2010
author: PipisCrew
date: 2017-07-25
categories: [news]
toc: true
---

Test data :
```js
30-Jun-2017 15:32
30-Jun-2017 14:22
26-Jun-2017 12:23
22-Jun-2017 13:03
22-Jun-2017 11:39
13-Jun-2017 15:35
07-Jun-2017 13:44
07-Jun-2017 12:47
05-Jun-2017 11:42
05-Jun-2017 11:27
02-Jun-2017 14:54
26-May-2017 17:12
26-May-2017 12:14
10-May-2017 11:33
28-Apr-2017 11:11
18-Apr-2017 12:37
13-Apr-2017 16:16
```

1-select the cells > rclick > Format Cells > Custom 
2-add the field type your can define a new pattern (dont worry the default patterns will not deleted), for the data we have, you have to enter :

```js
dd-mmm-yyyy hh:mm
```

3-goto B1 and enter 
```js
=TEXT(A1, "yyyy-mm-dd")
```
then apply it for all the cells by dragging it.

custom format by microsoft - https://support.office.com/en-us/article/Format-numbers-as-dates-or-times-418bd3fe-0577-47c8-8caa-b4d30c528309

> If you’re modifying a format that includes time values and you use "m" immediately after the "h" or "hh" code or immediately before the "ss" code, Excel displays minutes instead of the month.

https://support.office.com/en-us/article/Format-a-date-the-way-you-want-8e10019e-d5d8-47a1-ba95-db95123d273e

--

the buggy part comes, when you sit on a computer with **primary region & language** different than English.

you have to define the custom pattern on your own language and not as 
```js
dd-mmm-yyyy hh:mm
```

again we have a secret by microsoft. the solution is to enter the language LCID in hex, in front of the custom format (lol) so you go with :
```js
//src https://www.ablebits.com/office-addins-blog/2015/03/11/change-date-format-excel/
//backup http://docdroid.net/4xDx0Se
//LCID list - https://msdn.microsoft.com/en-us/library/cc233982.aspx
//backup LCID list - http://blog.csdn.net/2066/article/details/45555

//UK
[$-809]dd-mmm-yyyy hh:mm

//US
[$-409]dd-mmm-yyyy hh:mm
```

the LCID can be used on the formula. example :
```js
//https://sites.google.com/site/e90e50fx/home/Month-day-names-with-Excel-formula
=TEXT(A1,"[$-409]d mmmm yyyy")
```

for me still no working!

origin - http://www.pipiscrew.com/?p=9336 format-date-or-datetime-to-excel-2010