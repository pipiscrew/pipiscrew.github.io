---
title: o[bootstrap-table+php] transform html table to magic no2
author: PipisCrew
date: 2015-01-07
categories: []
toc: true
---

//line 15
![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap361.png "snap361")

//line 22
![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap362.png "snap362")

//line 101
![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap363.png "snap363")

```js
//test

<?php if="" ($_server['request_method']="" !='POST' )="" {="" session_destroy();="" echo=""?><center><form style='width:300px;margin-top:50px' method='post'>";

	if ($_GET["err"])
		echo "<div class='alert alert-danger'>Invalid Password</div>";

	echo "<input id='txt_password' name='txt_password' class='form-control'>  
";
	echo "<button class='btn btn-primary' type='submit' name='submit'>Login</button></form></center>";
	exit; 
}
else 
{
	if (!(isset($_POST["txt_password"]) && strtolower($_POST["txt_password"])=="123"))
	{
		session_destroy();

		//	die("catastrophic failure");
		header("Location: show_participants.php?err=1");
		exit;
	} else {
		$_SESSION["x"] = "123";
	}

}

// include DB
require_once ('config.php');

$db             = connect();

$cmb_rows = null;
$cmb_rows = getSet($db,"select distinct(app_name) from votes order by app_name DESC", null);
?>

			$(function() {

					//http://wenzhixin.net.cn/p/bootstrap-table/docs/examples.html#via-javascript-table
					$('#votes_tbl').bootstrapTable();

                     var jArray =   <?php echo json_encode($cmb_rows); ?>;

                     var the_rows = "<option></option>";
                     for (var i = 0; i < jArray.length; i++)
                     {
                        the_rows += "<option>" + jArray[i]["app_name"] + "</option>\r\n";
                     }

                     //set the contest rows
                     $("#cmb_contest").html(the_rows);

					$('#cmb_contest').on('change', function() {
					  $('#votes_tbl').bootstrapTable('refresh');
					});

			}); //jQuery ends

				//bootstrap-table
				function queryParamsVOTES(params)
				{
					var q = {
						"limit": params.limit,
						"offset": params.offset,
						"search": params.search,
						"name": params.sort,
						"order": params.order,
						//
						"contest": $("#cmb_contest").val()
					};

					return q;
				}

		<div style="width:300px">

			<select id="cmb_contest" class="form-control">
			</select>

		</div>

    <table id="votes_tbl" data-toggle="table" data-striped="true" data-url="show_participants_pagination.php" data-show-columns="true" data-search="true" data-show-refresh="true" data-show-toggle="true" data-pagination="true" data-click-to-select="true" data-single-select="true" data-page-size="50" data-height="800" data-side-pagination="server" data-query-params="queryParamsVOTES">

        <thead>
            <tr>
				<th data-field="state" data-checkbox="true">
				</th>

				<th data-field="id" data-visible="false">
					id
				</th>

				<th data-field="member_id" data-sortable="true">
					member_id
				</th>

				<th data-field="fullname" data-sortable="true">
					fullname
				</th>

				<th data-field="mail" data-sortable="true">
					mail
				</th>

				<th data-field="gender" data-sortable="true">
					gender
				</th>

				<th data-field="timezone" data-sortable="true">
					timezone
				</th>

				<th data-field="date_rec" data-sortable="true">
					date_rec
				</th>

				<th data-field="app_name" data-sortable="true">
					app_name
				</th>
            </tr>
        </thead>

        <tbody id="tbl_rows"></tbody>
    </table>

```

```js
//show_participants_pagination.php

session_start();

//check if logged in
if (!isset($_SESSION["x"])) {
    header("Location: show_participants.php");
    exit ;
}

.
.
.
.
$arr = array('total'=> $count_recs,'rows' => $rows);

header("Content-Type: application/json", true);

echo json_encode($arr);
```

origin - http://www.pipiscrew.com/?p=2153 bootstrap-tablephp-transform-html-table-to-magic-no2