---
title: Datatables example minimal 87kb dependencies
author: PipisCrew
date: 2020-03-18
categories: [js]
toc: true
---

```js

//https://datatables.net/

$(document).ready(function() {
    $('#main_table_countries').dataTable({
        "scrollCollapse": true,
        "order": [
            [1, 'desc']
        ],
        "sDom": '<"bottom"flp><"clear">',
        "paging": false
    });
});

<table id="main_table_countries" class="table table-bordered table-hover" cellspacing="0" text-align:left"="">
<thead>
    <tr>
        <th width="100">
            Country,  
Other
        </th>
        <th width="20">
            Total  
Cases
        </th>
        <th width="30">
            New  
Cases
        </th>
        <th width="30">
            Total  
Deaths
        </th>
        <th width="30">
            New  
Deaths
        </th>
        <th width="30">
            Active  
Cases
        </th>
        <th width="30">
            Total  
Recovered
        </th>
        <th width="30">
            Serious,  
Critical
        </th>
    </tr>
</thead>

 <tbody>
    <tr style="    ">
        <td style="font-weight: bold; font-size:15px; text-align:left; padding-left:3px;">
            China
        </td>
        <td style="font-weight: bold; text-align:right">
            80,430
        </td>
        <td style="font-weight: normal; text-align:right;background-color:#FFEEAA;">
            +160
        </td>
        <td style="font-weight: bold; text-align:right;">
            3,013
        </td>
        <td style="font-weight: bold; text-align:right; background-color:red; color:white ">
            +32
        </td>
        <td style="font-size:14px;text-align:right;font-weight:bold;">
            25,158
        </td>
        <td style="font-weight: bold; text-align:right">
            52,259
        </td>
        <td style="font-weight: bold; text-align:right">
            5,952
        </td>
    </tr>
    <tr style="    ">
        <td style="font-weight: bold; font-size:15px; text-align:left; padding-left:3px;">
            Italy
        </td>
        <td style="font-weight: bold; text-align:right">
            3,089
        </td>
        <td style="font-weight: normal; text-align:right;">
        </td>
        <td style="font-weight: bold; text-align:right;">
            107
        </td>
        <td style="font-weight: bold; text-align:right; ">
        </td>
        <td style="font-size:14px;text-align:right;font-weight:bold;">
            2,706
        </td>
        <td style="font-weight: bold; text-align:right">
            276
        </td>
        <td style="font-weight: bold; text-align:right">
            295
        </td>
    </tr>

    <tr style="background-color:#EAF7D5    ">
        <td style="font-weight: bold; font-size:15px; text-align:left; padding-left:3px;">
            Vietnam
        </td>
        <td style="font-weight: bold; text-align:right">
            16
        </td>
        <td style="font-weight: normal; text-align:right;">
        </td>
        <td style="font-weight: bold; text-align:right;">
        </td>
        <td style="font-weight: bold; text-align:right; ">
        </td>
        <td style="font-size:14px;text-align:right;font-weight:bold;">
            0
        </td>
        <td style="font-weight: bold; text-align:right">
            16
        </td>
        <td style="font-weight: bold; text-align:right">
        </td>
    </tr>
</tbody>

<tbody>
    <tr class="total_row">
        <td>
             **Total:** 
        </td>
        <td>
            96,979
        </td>
        <td style="background-color:#FFEEAA; color:#000;">
            1,811
        </td>
        <td>
            3,311
        </td>
        <td style="background-color:red; color:#fff">
            57
        </td>
        <td>
            39,685
        </td>
        <td>
            53,983
        </td>
        <td>
            6,422
        </td>
    </tr>
</tbody>
 </table>
```

author - https://sprymedia.co.uk/

* * *

[https://datatables.net/reference/api/rows().data()](https://datatables.net/reference/api/rows().data())

https://datatables.net/manual/data/

https://datatables.net/reference/option/

https://datatables.net/examples/ajax/objects.html

https://datatables.net/reference/option/ajax.data

https://github.com/DataTables/DataTables/tree/master/examples

origin - https://www.pipiscrew.com/?p=17283 datatables-example-minimal-87kb-dependencies