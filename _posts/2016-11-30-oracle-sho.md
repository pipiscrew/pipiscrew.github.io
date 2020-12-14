---
title: Oracle show tables schema
author: PipisCrew
date: 2016-11-30
categories: [sql]
toc: true
---

```js
--get all tables from dbase
SELECT * FROM ALL_OBJECTS WHERE OBJECT_TYPE = 'TABLE' 
AND OWNER='THE_OWNER' and temporary='N' order by object_name

--get columns info for a table
select column_name,data_type, data_length from ALL_TAB_COLUMNS 
where OWNER = 'THE_OWNER' and TABLE_NAME='TABLE' order by column_id
```

origin - http://www.pipiscrew.com/?p=6331 oracle-show-tables-schema