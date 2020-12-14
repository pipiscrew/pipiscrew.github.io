---
title: count rows for each table
author: PipisCrew
date: 2015-10-27
categories: [sql]
toc: true
---

![snap171](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap171.png)

```js
select t.name TableName, i.rows Records
from sysobjects t, sysindexes i
where t.xtype = 'U' and i.id = t.id and i.indid in (0,1)
order by Records DESC;
```

origin - http://www.pipiscrew.com/?p=2276 sql-count-rows-for-each-table