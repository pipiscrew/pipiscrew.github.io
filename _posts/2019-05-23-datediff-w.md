---
title: datediff with in operator
author: PipisCrew
date: 2019-05-23
categories: [sql]
toc: true
---

```js
select * from table
where daterec is not null and DATEDIFF(d, daterec ,getdate()) in (5,12)
```

origin - https://www.pipiscrew.com/?p=14934 datediff-with-in-operator