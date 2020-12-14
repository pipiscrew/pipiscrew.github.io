---
title: o[mysql+php+js] refresh second combo when depends on first combo
author: PipisCrew
date: 2014-12-23
categories: []
toc: true
---

```js

	$(function (){

		////////////////////////////////////////
		// MODAL FUNCTIONALITIES [START]
		//when modal closed, hide the warning messages + reset
		$('#modalEXPENSES').on('hidden.bs.modal', function()
			{
				//clear sub categories combo
				$("#expense_sub_category_id").html("");

				//when close - clear elements
				$('#formEXPENSES').trigger("reset");

				//clear validator error on form
				validatorEXPENSES.resetForm();
			});

		//add new - subcategory modal - hide event - reset field
		$('#modalEXPENSESsubcat').on('hidden.bs.modal', function() {
				//refresh the combo
		    	refresh_subcategory_by_categoryVAL();

		        //clear elements
		        $('#formEXPENSESsubcat').trigger("reset");
		});

		//functionality when the modal already shown and its long, when reloaded scroll to top
		$('#modalEXPENSES').on('shown.bs.modal', function()
			{
				$(this).animate(
					{
						scrollTop : 0
					}, 'slow');
			});
		// MODAL FUNCTIONALITIES [END]
		////////////////////////////////////////

		//when combo category change
		$('[name=expense_category_id]').on('change', function()
		{
			refresh_subcategory_by_categoryVAL();
		});

		//when combo sub_category change
		$('[name=expense_sub_category_id]').on('change', function()
		{
			//check if is first option **add new**
			if ($(this).val()=="-1")
			{
				//set modal parentID
				$("#subcat_parent_id").val($("#expense_category_id").val());

				//show modal to add new sub category
				$('#modalEXPENSESsubcat').modal('toggle');
			}

		});

		////////////////////////////////////////
		// MODAL SUBMIT aka save & update button
		$('#formEXPENSES').submit(function(e)
			{
				e.preventDefault();

				////////////////////////// validation
				var form = $(this);
				form.validate();

				if (!form.valid())
				return;
				////////////////////////// validation

				var postData = $(this).serializeArray();
				var formURL = $(this).attr("action");

				//close modal
				$('#modalEXPENSES').modal('toggle');

				$.ajax(
					{
						url : formURL,
						type: "POST",
						data : postData,
						success:function(data, textStatus, jqXHR)
						{
							if (data=="00000")
							//refresh
							$('#expenses_tbl').bootstrapTable('refresh');
							else
							alert("ERROR");
						},
						error: function(jqXHR, textStatus, errorThrown)
						{
							alert("ERROR - connection error");
						}
					});
			});

		////////////////////////////////////////
		// MODAL SUBMIT aka save & update button
		$('#formEXPENSESsubcat').submit(function(e)
			{
				e.preventDefault();

				////////////////////////// validation
				var form = $(this);
				form.validate();

				if (!form.valid())
				return;
				////////////////////////// validation

				var postData = $(this).serializeArray();
				var formURL = $(this).attr("action");

				$.ajax(
					{
						url : formURL,
						type: "POST",
						data : postData,
						success:function(data, textStatus, jqXHR)
						{
							if (data=="00000")
							{
								$('#modalEXPENSESsubcat').modal('toggle');
							}
							else
								alert("ERROR");
						},
						error: function(jqXHR, textStatus, errorThrown)
						{
							alert("ERROR - connection error");
						}
					});
			});

	}); //jQuery

	//universal function to fill combos
	function setComboItems(ctl_name, jArray)
	{
		var combo_rows = "<option value='0'></option><option value='-1'>**Add new**</option>";
		for (var i = 0; i < jArray.length; i++)
		{
			combo_rows += "<option value='" + jArray[i]["id"] + "'>" + jArray[i]["description"] + "</option>";
		}

		$("[name=" + ctl_name + "]").html(combo_rows);
		$("[name=" + ctl_name + "]").change();
	}

	function refresh_subcategory_by_categoryVAL(sub_category)
	{
		//used when edit a record
		var sub_category_id;
		sub_category_id = sub_category;
		//used when edit a record

		$.ajax(
			{
				url : 'x_get_by_category.php',
				dataType : 'json',
				type : 'POST',
				data :
				{
					"id" : $("#expense_category_id").val(),
				},
				success : function(data)
				{
					setComboItems("expense_sub_category_id",data.recs);

					if (sub_category_id)
					{	
						$('[name=expense_sub_category_id]').val(sub_category_id);

						if (sub_category_id!= 0 && $('[name=expense_sub_category_id]').val()==null)
							alert("Subcategory record cant be found!");
					}	

				},
				error : function(e)
				{
					alert("error");
				}
			});
	}

[/javascript]

//sample who call **refresh_subcategory_by_categoryVAL** using parameter
```js
	//edit button - read record
	function query_EXPENSES_modal(rec_id)
	{
		loading.appendTo(document.body);

		$.ajax(
			{
				url : "x_fetch.php",
				type: "POST",
				data :
				{
					expense_id : rec_id
				},
				success:function(data, textStatus, jqXHR)
				{
					loading.remove();

					if (data!='null')
					{
						$("[name=expensesFORM_updateID]").val(data.expense_id);
						$('[name=expense_category_id]').val(data.expense_category_id);
						refresh_subcategory_by_categoryVAL(data.expense_sub_category_id);

						$('[name=expense_daterec]').val(data.expense_daterec);
						$('[name=price]').val(data.price);
						$('[name=comment]').val(data.comment);

						$('#lblTitle_EXPENSES').html("Edit Expense");
						$('#modalEXPENSES').modal('toggle');
					}
					else
					alert("ERROR - Cant read the record.");
				},
				error: function(jqXHR, textStatus, errorThrown)
				{
					loading.remove();
					alert("ERROR");
				}
			});
	}
[/javascript]
```js
//html

<div class="modal fade" id="modalEXPENSES" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
	<div class="modal-dialog">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal" aria-hidden="true">
					×
				</button>

#### 
					New Expense

			</div>
			<div class="modal-body">
				<form id="formEXPENSES" role="form" method="post" action="x_save.php">

					<div class='form-group'>
						<label>
							Category :
						</label>
						<select id="expense_category_id" name='expense_category_id' class='form-control'></select>
					</div>

					<div class='form-group'>
						<label>
							Subcategory :
						</label>
						<select id="expense_sub_category_id" name='expense_sub_category_id' class='form-control'></select>
					</div>

					<input name="parent_id" id="parent_id" class="form-control" style="display:none;">
					<input name="expensesFORM_updateID" id="expensesFORM_updateID" class="form-control" style="display:none;">

					<div class="modal-footer">
						<button id="bntCancel_EXPENSES" type="button" class="btn btn-default" data-dismiss="modal">
							cancel
						</button>
						<button id="bntSave_EXPENSES" class="btn btn-primary" type="submit" name="submit">
							save
						</button>
					</div>
				</form>
			</div>
		</div>
	</div>
</div>

<div class="modal fade" id="modalEXPENSESsubcat" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
	<div class="modal-dialog">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal" aria-hidden="true">
					×
				</button>

#### 
					New Subcategory

			</div>
			<div class="modal-body">
				<form id="formEXPENSESsubcat" role="form" method="post" action="x_new_sub_save.php">

					<div class='form-group'>
						<label>
							Subcategory :
						</label>
						<input id="subcategory_txt" name='subcategory_txt' class='form-control'>
					</div>

					<input name="subcat_parent_id" id="subcat_parent_id" class="form-control" style="display:none;">

					<div class="modal-footer">
						<button id="bntCancel_EXPENSESsubcat" type="button" class="btn btn-default" data-dismiss="modal">
							cancel
						</button>
						<button id="bntSave_EXPENSESsubcat" class="btn btn-primary" type="submit" name="submit">
							save
						</button>
					</div>
				</form>
			</div>
		</div>
	</div>
</div>

```

```js
//x_get_by_category.php
<?php session_start();="" if(!isset($_session["u"]))="" {="" header("location:="" login.php");="" exit="" ;="" }="" include="" db="" require_once="" ('config.php');="" if(!isset($_post["id"])){="" echo="" json_encode(null);="" return;="" }="" $id="$_POST["id"];" $db="connect();" $recs="getSet($db,"select" expense_category_id="" as="" id,expense_category_name="" as="" description="" from="" expense_categories="" where="" parent_id="?",array($id));" $json="array('recs'="?> $recs);

header("Content-Type: application/json", true);

echo json_encode($json);

//x_new_sub_save.php
<?php session_start();="" if="" (!isset($_session["u"]))="" {="" header("location:="" login.php");="" exit="" ;="" }="" else="" if="" ($_session['level']!="9)" {="" die("you="" are="" not="" authorized="" to="" view="" this!");="" }="" if="" (!isset($_post['subcat_parent_id'])="" ||="" !isset($_post['subcategory_txt'])){="" echo="" "error010101010";="" return;="" }="" db="" require_once="" ('config.php');="" $db="connect();" $sql="INSERT INTO expense_categories (parent_id, expense_category_name) VALUES (:parent_id, :expense_category_name)" ;="" $stmt="$db-"?>prepare($sql);

$stmt->bindValue(':parent_id' , $_POST['subcat_parent_id']);
$stmt->bindValue(':expense_category_name' , $_POST['subcategory_txt']);

$stmt->execute();

echo $stmt->errorCode();

?>
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap357.png "snap357")

![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap358.png "snap358")

![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap360.png "snap360")

origin - http://www.pipiscrew.com/?p=2139 mysqlphpjs-refresh-second-combo-when-depends-on-first-combo