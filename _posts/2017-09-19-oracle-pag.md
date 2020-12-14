---
title: Oracle pagination
author: PipisCrew
date: 2017-09-19
categories: [sql]
toc: true
---

```js
--http://viralpatel.net/blogs/oracle-pagination-using-rownum-limiting-result-set/
  select * 
      from ( select a.*, rownum rnum
         from ( select * from the_owner.x where IDENTIFIER='1' and source = 'x' order by 1) a
         ) 
    where rnum > 3 and rnum < 15
```

origin - http://www.pipiscrew.com/?p=9990 oracle-pagination