---
title: o[excel] vlookup - compare columns
author: PipisCrew
date: 2018-01-29
categories: [app]
toc: true
---

in nutshell

<center>
![alt](https://i.imgur.com/8zVlvKH.png)

![alt](https://i.imgur.com/Jz24SZo.png)

![alt](https://i.imgur.com/x18MWbQ.png)
</center>

* * *

reference - [http://www.mrexcel.com/forum/excel-questions/5129-vlookup-copying-formula-down-whole-column.html#post22660](http://www.mrexcel.com/forum/excel-questions/5129-vlookup-copying-formula-down-whole-column.html#post22660)

![snap203](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap203.png)

```js

=VLOOKUP(E193;$A$1:$A$627;1;FALSE)

```

E193 = is the column with fewer values.
A1:A627 = is the column with most values.
1 = the column number in table from which the matching value must be returned. The first column is 1.
FALSE = (Optional) Enter FALSE to find an exact match. Enter TRUE (default) to find an approximate match.

the $sign take place when dragging the first cell dont change this value

create the formula on top cell then drag it till bottom

* * *

## End of Excel VLOOKUPS – Power Pivot Relationships

[https://blogs.msdn.microsoft.com/microsoft_press/2016/03/16/from-the-mvps-end-of-excel-vlookups-power-pivot-relationships/](https://blogs.msdn.microsoft.com/microsoft_press/2016/03/16/from-the-mvps-end-of-excel-vlookups-power-pivot-relationships/)

origin - http://www.pipiscrew.com/?p=4088 excel-vlookup-compare-columns