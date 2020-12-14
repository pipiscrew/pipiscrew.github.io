---
title: Oracle query by date field
author: PipisCrew
date: 2016-11-30
categories: [sql]
toc: true
---

```js
--ref http://stackoverflow.com/q/9180014
select cust_id from THE_OWNER.SAP_DEV 
where SAP_DEV.lastmodified between TO_DATE('24/11/2016 00:00:00', 'DD/MM/YYYY HH24:MI:SS') and TO_DATE('24/11/2016 23:59:59', 'DD/MM/YYYY HH24:MI:SS')
order by cust_id desc;
```

origin - http://www.pipiscrew.com/?p=6317 oracle-query-by-date-field