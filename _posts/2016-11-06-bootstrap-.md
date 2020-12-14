---
title: o[bootstrap-table] use of data-sort-name
author: PipisCrew
date: 2016-11-06
categories: [js]
toc: true
---

When user press a column to sort, define another column as source.

```js
//http://jsfiddle.net/e3nk137y/9602/
<table data-toggle="table">
    <thead>
        <tr>
            <th data-field="fruit" data-sortable="true">Item</th>
            <th data-field="date" data-sort-name="dateval" data-sortable="true">Date</th>
            <th data-field="type" data-sortable="true">Type</th>
            <th data-field="dateval" data-sortable="true" data-visible="false">DateVAL</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Pear </td>
            <td>January</td>
            <td>Fruit</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Carrot</td>
            <td>March</td>
            <td>Vegetable</td>
            <td>3</td>
        </tr>
        <tr>
            <td>Apple </td>
            <td>February</td>
            <td>Fruit</td>
            <td>2</td>
        </tr>
    </tbody>
</table>
```

doc - http://bootstrap-table.wenzhixin.net.cn/documentation/

origin - http://www.pipiscrew.com/?p=6247 bootstrap-table-use-of-data-sort-name