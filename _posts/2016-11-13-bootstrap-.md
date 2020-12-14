---
title: o[bootstrap-table] transform PHP recordset to magic!
author: PipisCrew
date: 2016-11-13
categories: [js,php]
toc: true
---

```js
//test
<?php
	$db = connect();
	$recs = getSet($db,"select id,created,seller,total_cost,type from customers", null);
?>

	$(function() {
			///////////////////////////////////////////////////////////// FILL table
			var jArray_recs =   <?php echo json_encode($recs); ?>; //convert PHP variable to JSON

			//enumerate the records
			var tbl_recs = "";
			for (var i = 0; i < jArray_recs.length; i++)
			{
				tbl_recs += "<tr>" +
				"<td>" + jArray_recs[i]["id"] + "</td>" + 
				"<td>" + jArray_recs[i]["created"] + "</td>" +
				"<td>" + jArray_recs[i]["seller"] + "</td>" + 
				"<td>" + jArray_recs[i]["total_cost"] + "</td>"
				"<td>" + jArray_recs[i]["type"] + "</td></tr>";
			}

			$("#tbl_rows").html(tbl_recs); //set to table
			///////////////////////////////////////////////////////////// FILL table

			$("#tbl").bootstrapTable(); //transform to magic!
		})

<table id="tbl" data-striped=true>
	<thead>
		<tr>
			<th data-field="id" data-visible="false">ID</th>
			<th data-sortable="true">Created</th>
			<th data-sortable="true">Seller</th>
			<th data-sortable="true">Total Cost</th>
			<th data-sortable="true">Type</th>
		</tr>
	</thead>

	<tbody id="tbl_rows"></tbody>
</table>
```

doc - http://bootstrap-table.wenzhixin.net.cn/documentation

* * *

```js
//is invalid way to use data-sort-name on TH, but add it here coz
//return all data attributes with _date_data
//http://jsfiddle.net/e3nk137y/1434/
<th data-field="date"  data-sortable="true" data-sort-name="_date_data" data-sorter="monthSorter">Date</th>
```

origin - http://www.pipiscrew.com/?p=6248 bootstrap-table-transform-php-recordset-to-magic