---
title: o[linq] Query a datatable with linq
author: PipisCrew
date: 2016-07-21
categories: [.net]
toc: true
---

```js
DataTable tbl_N = conn.GetDATATABLE("select * from tbl where convert (varchar(10),addedDate,120)= '" + DateTime.Today.ToString("yyyy-MM-dd") + "' and thefield ='N'");
var tbl = tbl_N.AsEnumerable().
Where(row => row.Field<string>("fieldA") != null && row.Field<string>("fieldA") == "soccer" && string.IsNullOrEmpty(row.Field<string>("fieldB"))).ToList();

            foreach (DataRow item in tbl_N_Phrama_Count)
       {
       not_proceed+=item["field88"] + ", ";
       }

//plain count
int tbl_Count= tbl_N.AsEnumerable().
Count(row => row.Field<string>("fieldA") != null && row.Field<string>("fieldA") == "soccer" && string.IsNullOrEmpty(row.Field<string>("fieldB")));
```

origin - http://www.pipiscrew.com/?p=5914 linq-query-a-datatable-with-linq