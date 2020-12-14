---
title: serialize input file via jQuery Form Plugin
author: PipisCrew
date: 2015-09-09
categories: [js,php]
toc: true
---

jQuery doesnt support POST file input, today we will use #jQuery Form Plugin#

using 
[http://jquery.malsup.com/form/#file-upload](http://jquery.malsup.com/form/#file-upload)

```js

$(function() {
	$('#formAFFILIATED').ajaxForm({ 
		beforeSend: function() {
		  loading.appendTo($('#formAFFILIATED'));
		},
		 complete: function(xhr) {
			loading.remove();

			data = xhr.responseText;

			console.log(data);
			loading.remove();

			if (data=="00000")
			{	//refresh
				$('#affiliated_tbl').bootstrapTable('refresh');

				//close modal
				$('#modalAFFILIATED').modal('toggle');
			}

		}
	}); 
}); 

<form id="formAFFILIATED" role="form" method="post" action="tab_affiliated_save.php">

	<div class='form-group'>
		<label>affiliated_title :</label>
		<input name='affiliated_title' class='form-control' placeholder='affiliated_title'>
	</div>

	<input type="file" name="affiliated_fileToUpload" id="affiliated_fileToUpload">

	<input name="affiliatedFORM_updateID" id="affiliatedFORM_updateID" class="form-control" style="display:none;">

	<div class="modal-footer">
		<button id="bntCancel_AFFILIATED" type="button" class="btn btn-default" data-dismiss="modal">
			cancel
		</button>
		<button id="bntSave_AFFILIATED" class="btn btn-primary" type="submit" name="submit">
			save
		</button>
	</div>
</form>
```

```js
//image
//validate is true image
if (getimagesize($_FILES["affiliated_fileToUpload"]["tmp_name"])==0){
    echo "Sorry, there was an error uploading your file.";
    return;
}

if (sizeof($_FILES)==0){
    echo "Please, choose a file";
    return;
}

//when isnot required field
if (sizeof($_FILES)) {
	$target_dir = "../affiliated_img/"; // a dir back
	$target_file = $target_dir . basename($_FILES["affiliated_fileToUpload"]["name"]);

	if (move_uploaded_file($_FILES["affiliated_fileToUpload"]["tmp_name"], $target_file)) {
		echo "The file ". basename( $_FILES["fileToUpload"]["name"]). " has been uploaded.";
	} else {
		echo "Sorry, there was an error uploading your file.";
	}
}
//image
.
.
.
//sql transaction
echo $stmt->errorCode(); 
```

^var_dump($FILES)
```js
array(1) {
  ["affiliated_fileToUpload"]=>
  array(5) {
    ["name"]=>
    string(17) "x.png"
    ["type"]=>
    string(9) "image/png"
    ["tmp_name"]=>
    string(18) "/var/tmp/phplkS4RO"
    ["error"]=>
    int(0)
    ["size"]=>
    int(6924)
  }
}
```

origin - http://www.pipiscrew.com/?p=1897 php-serialize-input-file-via-jquery-form-plugin