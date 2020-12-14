---
title: Dynamic List<T> Where
author: PipisCrew
date: 2016-06-21
categories: [.net]
toc: true
---

query Dynamic List<t> -- List<dynamic>

we have a function returns List<dynamic>
![snap623](https://www.pipiscrew.com/wp-content/uploads/2016/06/snap623.png)

in debug mode filled by :
![snap620](https://www.pipiscrew.com/wp-content/uploads/2016/06/snap620.png)

normally we will write :
![snap621](https://www.pipiscrew.com/wp-content/uploads/2016/06/snap621.png)

this will throw an exception like :
![snap622](https://www.pipiscrew.com/wp-content/uploads/2016/06/snap622.png)

the solution is to use reflection :
```js
object d = ComTaxOffice.GetTaxOffices().FirstOrDefault(p => p.GetType().GetProperty("TaxOfficeId").GetValue(p, null).ToString() == "3");
```</dynamic></dynamic></t>

origin - http://www.pipiscrew.com/?p=5870 dynamic-list-where