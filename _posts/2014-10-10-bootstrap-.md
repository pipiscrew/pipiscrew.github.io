---
title: o[bootstrap-table] transform html table to magic
author: PipisCrew
date: 2014-10-10
categories: []
toc: true
---

reference : [http://wenzhixin.net.cn/p/bootstrap-table/docs/documentation.html](http://wenzhixin.net.cn/p/bootstrap-table/docs/documentation.html)
**the css**
```js
		<style>
			/*jquery.validate*/
			label.error { color: #FF0000; font-size: 11px; display: block; width: 100%; white-space: nowrap; float: none; margin: 8px 0 -8px 0; padding: 0!important; }

			/*bootstrap-table selected row*/
			.fixed-table-container tbody tr.selected td	{ background-color: #B0BED9; }

			/*progress*/
			.modal-backdrop { opacity: 0.7;	filter: alpha(opacity=70);	background: #fff; z-index: 2;}
			div.loading { position: fixed; margin: auto; top: 0; right: 0; bottom: 0; left: 0; width: 200px; height: 30px; z-index: 3; }
		</style>
```

**the php**
```js
<?php include="" db="" require_once="" ('config.php');="" $db="connect();" $rows="null;" read="" rows="" $rows="getSet($db,"select" offer_id,="" date_format(offer_date_rec,'%d-%m-%y')="" as="" date_created,="" users.fullname="" as="" user="" from="" offers="" left="" join="" users="" on="" users.user_id="offers.offer_seller_id" where="" company_id="?" order="" by="" offer_date_rec="" desc",="" array($_get['id']));="" read="" rows=""?>
```

**the javascript**
```js

    $(function() {
					 ///////////////////////////////////////////////////////////// FILL rows grid
					 var jArray_rows =   <?php echo json_encode($rows); ?>;

					 var the_rows = "";
					 for (var i = 0; i < jArray_rows.length; i++)
					 {
					 	the_rows += "<tr><td></td><td>" + jArray_rows[i]["offer_id"] + "</td><td>" + jArray_rows[i]["date_created"] + "</td>" +
					 	"<td>" + jArray_rows[i]["user"] + "</td></tr>";
					 }

					 //set the table rows
					 $("#tbl_rows").html(the_rows);
					 ///////////////////////////////////////////////////////////// FILL rows grid

					 //transform html to magic!
					 $("#tbl").bootstrapTable();

					 //edit button - get the record ID!
					 $('#btn_edit').on('click', function(e)
					 	{
					 		e.preventDefault();

					 		var row = $('#tbl').bootstrapTable('getSelections');

					 		if (row.length>0)
					 		{
					 			console.log(row[0].id);
					 		}
					 		else
								alert("Please select a row");
					 	})

	})				 

```

**the html**
```js
		<div class="container">

			<button id="btn_edit" type="button" class="btn btn-primary">
				Edit
			</button>

			<table id="tbl" data-striped="true" data-click-to-select="true" data-single-select="true">
				<thead>
					<tr>
						<th data-field="state" data-checkbox="true"></th>

						<th data-field="id" data-visible="false">ID</th>

						<th data-sortable="true">Created</th>
						<th data-sortable="true">Seller</th>
						<th data-sortable="true">Total Cost</th>
						<th data-sortable="true">Type</th>
					</tr>
				</thead>

				<tbody id="tbl_rows"></tbody>
			</table>

		</div>
```

**in one page :**
```js
<?php include="" db="" require_once="" ('config.php');="" $db="connect();" $rows="null;" read="" rows="" $rows="getSet($db,"select" offer_id,="" date_format(offer_date_rec,'%d-%m-%y')="" as="" date_created,="" users.fullname="" as="" user="" from="" offers="" left="" join="" users="" on="" users.user_id="offers.offer_seller_id" where="" company_id="?" order="" by="" offer_date_rec="" desc",="" array($_get['id']));="" read="" rows=""?>

		<style>
			/*jquery.validate*/
			label.error { color: #FF0000; font-size: 11px; display: block; width: 100%; white-space: nowrap; float: none; margin: 8px 0 -8px 0; padding: 0!important; }

			/*bootstrap-table selected row*/
			.fixed-table-container tbody tr.selected td	{ background-color: #B0BED9; }

			/*progress*/
			.modal-backdrop { opacity: 0.7;	filter: alpha(opacity=70);	background: #fff; z-index: 2;}
			div.loading { position: fixed; margin: auto; top: 0; right: 0; bottom: 0; left: 0; width: 200px; height: 30px; z-index: 3; }
		</style>

    $(function() {
					 ///////////////////////////////////////////////////////////// FILL rows grid
					 var jArray_rows =   <?php echo json_encode($rows); ?>;

					 var the_rows = "";
					 for (var i = 0; i < jArray_rows.length; i++)
					 {
					 	the_rows += "<tr><td></td><td>" + jArray_rows[i]["offer_id"] + "</td><td>" + jArray_rows[i]["date_created"] + "</td>" +
					 	"<td>" + jArray_rows[i]["user"] + "</td></tr>";
					 }

					 //set the table rows
					 $("#tbl_rows").html(the_rows);
					 ///////////////////////////////////////////////////////////// FILL rows grid

					 //transform html to magic!
					 $("#tbl").bootstrapTable();

					 //edit button - get the record ID!
					 $('#btn_edit').on('click', function(e)
					 	{
					 		e.preventDefault();

					 		var row = $('#tbl').bootstrapTable('getSelections');

					 		if (row.length>0)
					 		{
					 			console.log(row[0].id);
					 		}
					 		else
								alert("Please select a row");
					 	})

	})				 

		<div class="container">

			<button id="btn_edit" type="button" class="btn btn-primary">
				Edit
			</button>

			<table id="tbl" data-striped="true" data-click-to-select="true" data-single-select="true">
				<thead>
					<tr>
						<th data-field="state" data-checkbox="true"></th>

						<th data-field="id" data-visible="false">ID</th>

						<th data-sortable="true">Created</th>
						<th data-sortable="true">Seller</th>
					</tr>
				</thead>

				<tbody id="tbl_rows"></tbody>
			</table>

		</div>
```

origin - http://www.pipiscrew.com/?p=1478 bootstrap-table-transform-html-table-to-magic