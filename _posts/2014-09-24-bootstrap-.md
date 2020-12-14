---
title: o[bootstrap] modal form - post with jquery ajax
author: PipisCrew
date: 2014-09-24
categories: []
toc: true
---

the modal form somewhere hidden in html :

```js

<div class="modal fade bs-modal-lg" id="modaloSUBSECTOR" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
	<div class="modal-dialog modal-lg">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal" aria-hidden="true">
					×
				</button>

#### New Sub Sector

			</div>
			<div class="modal-body">
				<form id="formoSUBSECTOR" role="form" method="post" action="test.php">

						<div class='form-group'>
							<label>Parent Sector :</label>
							<select id="oSECTOR_description" name='oSECTOR_description' class='form-control' readonly>
							</select>
						</div>

						<div class='form-group'>
							<label>Sub Sector Name :</label>
							<input id='oSUBSECTOR_name' name='oSUBSECTOR_name' class='form-control' placeholder='Sub Sector Name'>
						</div>

						<div class="modal-footer">
							<button id="bntCancel_oSUBSECTOR" type="button" class="btn btn-default" data-dismiss="modal">
								cancel
							</button>
							<button id="bntSave_oSUBSECTOR" class="btn btn-primary" type="submit" name="submit">
								save
							</button>
						</div>

				</form>
			</div>
		</div>
	</div>
</div>

```

the JS code :
```js

			////////////////////////////////////////
			// MODAL FUNCTIONALITIES [START]
			//when modal closed, hide the warning messages + reset
			$('#modaloSUBSECTOR').on('hidden.bs.modal', function() {
				//when close - clear elements
				$('#formoSUBSECTOR').trigger("reset");

				//clear validator error on form
				validatorSUBSECTOR.resetForm();
			});

			//functionality when the modal already shown and its long, when reloaded scroll to top
			$('#modaloSUBSECTOR').on('shown.bs.modal', function() {
				$(this).animate({
					scrollTop : 0
				}, 'slow');
			});
			// MODAL FUNCTIONALITIES [END]
			////////////////////////////////////////

			//jquery.validate.min.js
			var validatorSUBSECTOR = $("#formoSUBSECTOR").validate({
				rules : {
					 oSUBSECTOR_name : { 
						required : true,
						minlength : 2,
						maxlength : 100
					 },
					oSECTOR_description : { greaterThanZero : true }

				},
				messages : {
					oSECTOR_description : 'Required Field',
					oSUBSECTOR_name : 'Required Field'
				}
			});

		////////////////////////////////////////
		// MODAL SUBMIT aka save button
		$('#formoSUBSECTOR').submit(function(e) {
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
			$('#modaloSUBSECTOR').modal('toggle');

		    $.ajax(
		    {
		        url : formURL,
		        type: "POST",
		        data : postData,
		        success:function(data, textStatus, jqXHR) 
		        {
		            if (data=="ok")
		            	//update gui here
		            else
		             	alert("ERROR");
		        },
		        error: function(jqXHR, textStatus, errorThrown) 
		        {
		            alert("ERROR");      
		        }
		    });
		});
```

the PHP file called by form
```js
<?php
session_start();

if (!isset($_SESSION["x"])) {
	header("Location: x.html");
	exit ;
}

if(!isset($_POST['oSECTOR_description']) || !isset($_POST['oSUBSECTOR_name'])){
	echo "error";
	return;
}

//DB
require_once ('config.php');

$db = connect();

$sql = "INSERT INTO x (x, x) VALUES (:client_sector_sub_name, :client_sector_id)";
$stmt = $db->prepare($sql);

$stmt->bindValue(':client_sector_sub_name' , $_POST['oSUBSECTOR_name']);
$stmt->bindValue(':client_sector_id' , $_POST['oSECTOR_description']);

$stmt->execute();

$res = $stmt->rowCount();

if($res == 1)
	echo "ok";
else
	echo "error";
?>
```

origin - http://www.pipiscrew.com/?p=1369 bootstrap-modal-form-post-with-jquery-ajax