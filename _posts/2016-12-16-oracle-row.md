---
title: Oracle rownum (sql top) proper use
author: PipisCrew
date: 2016-12-16
categories: [sql]
toc: true
---

ROWNUM is a pseudocolumn (not a real column) that is available in a query. ROWNUM will be assigned the numbers 1, 2, 3, 4, ... N , where N is the number of rows.

```js
--when running this, you will realize that the order by doesnt take place
select * from owner.customers where rownum < 232 order by lastmodified desc
```

```js
--proper is :
select *
  from 
(select * 
   from owner.customers order by lastmodified desc)
 where ROWNUM < 232;
```

source - http://www.oracle.com/technetwork/issue-archive/2006/06-sep/o56asktom-086197.html

origin - http://www.pipiscrew.com/?p=6384 oracle-rownum-sql-top-proper-use