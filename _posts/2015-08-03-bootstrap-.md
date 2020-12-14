---
title: o[bootstrap] select mutliselect
author: PipisCrew
date: 2015-08-03
categories: []
toc: true
---

[http://github.com/davidstutz/bootstrap-multiselect](http://github.com/davidstutz/bootstrap-multiselect)

the following examples tested on **v0.9.13**

**w/ 'Server-Side' support**
[http://davidstutz.github.io/bootstrap-multiselect/#post](http://davidstutz.github.io/bootstrap-multiselect/#post)

```js

	$('#d_typies').multiselect({
		includeSelectAllOption: true,
		enableFiltering: true
	});

	<select class="form-control" id="d_typies" multiple="multiple" name="d_typies[]">
		<option value="1">test1
		<option value="2">test2
		<option value="3">test3
	 </select>
```

when **var_dump(d_typies)** at php :
```js
//outputs :
array(3) { [0]=> string(1) "1" [1]=> string(1) "2" [2]=> string(1) "3" }
```

* * *

[http://davidstutz.github.io/bootstrap-multiselect/#methods](http://davidstutz.github.io/bootstrap-multiselect/#methods)

```js
	$('#modalPRODUCT_SIZE_TIES').on('hidden.bs.modal', function() {
		//when close - clear elements
		$('#formPRODUCT_SIZE_TIES').trigger("reset");

		//deselect all + update button text
		$('#product_tie_size_id').multiselect('deselectAll', false);
		$('#product_tie_size_id').multiselect('updateButtonText', true);
	});
```

when save 
```js
if (isset($_POST['product_tie_size_id']))
	die("error");

$size_ids = $_POST['product_tie_size_id'];

//save.php - delete any tie for this template id, then re-save
executeSQL($db,"delete from product_size_ties where product_size_template_id=?",array($_POST["product_size_template_id"]),null);

if ($stmt = $db->prepare($sql)) {

	foreach($size_ids as $id) {
		$stmt->bindValue(':product_size_template_id' , $_POST['product_size_template_id']);
		$stmt->bindValue(':product_size_id' , $id);
		$stmt->execute();

		if ($stmt->errorCode() != "00000")
			die ("error on " + $id);
	}
}
```

when save (extended)
```js
.
.
$stmt->execute();

$res = $stmt->errorCode(); 

if ($res=="00000")
{
	if ($trans_type==0)
		$post_id =$db->lastInsertId();
	else 
	{
		$post_id = $_POST['postsFORM_updateID'];

		//when update delete all to FK table! 		
		executeSQL($db, "delete from post_categories where post_id=?", array($post_id));
	}

	//get categories
	$categories = $_POST['cmb_categories'];

	if (isset($categories)) {

		$sql = "INSERT INTO post_categories (post_id, category_id) VALUES (:post_id, :category_id)";
		if ($stmt = $db->prepare($sql)){

			foreach ($categories as $category_id) {

				$stmt->bindValue(':post_id' , $post_id);
				$stmt->bindValue(':category_id' , $category_id);

				$stmt->execute();	

				if($stmt->errorCode() != "00000"){
					echo $stmt->errorCode();
					exit;
				}
			}
		}

	}	
}

echo $res;
```

when fetch
```js
//edit button - read record
function query_PRODUCT_SIZE_TIES_modal(rec_id){
	loading.appendTo(document.body);

	$.ajax(
	{
		url : "fetch.php",
		type: "POST",
		data : { product_size_tie_id : rec_id },
		success:function(data, textStatus, jqXHR)
		{
			loading.remove();

			if (data!='null')
			{
				$("[name=product_size_tiesFORM_updateID]").val(data.rec_detail.product_size_tie_id);
				$('[name=product_size_template_id]').val(data.rec_detail.product_size_template_id);
//set selected								
				$('#product_tie_size_id').multiselect('select', data.rec_children);
				//console.log(data.rec_children);

				$('#lblTitle_PRODUCT_SIZE_TIES').html("Edit PRODUCT_SIZE_TIES");
				$('#modalPRODUCT_SIZE_TIES').modal('toggle');
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
```

```js
//fetch.php
try {

	$db = connect();

	$r= getRow($db, "SELECT product_size_tie_id, product_size_template_id, product_size_id FROM product_size_ties where product_size_tie_id=?", array($_POST['product_size_tie_id']));

	//construct an array of children id records (fallback to JS)
	$child = getSet($db, "select product_size_id from product_size_ties where product_size_template_id=?",array($r['product_size_template_id']));

	$rec_children = array();
	foreach($child as $row) {
		$rec_children[]= $row['product_size_id'];
	}

	//unicode
	header("Content-Type: application/json", true);
	echo json_encode(array("rec_detail" =>$r,"rec_children" => $rec_children));

} catch (Exception $e) {
    echo json_encode(null);
}
```

<center>

## advance example

</center>

[![](https://www.pipiscrew.com/wp-content/uploads/2015/06/snap246.png "snap246")](https://www.pipiscrew.com/wp-content/uploads/2015/06/snap246.png)

 [http://gist.github.com/pipiscrew/3bb8a7abfea372dc7745](http://gist.github.com/pipiscrew/3bb8a7abfea372dc7745)

origin - http://www.pipiscrew.com/?p=3134 bootstrap-select-mutliselect