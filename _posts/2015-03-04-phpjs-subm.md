---
title: o[php+js] submit a file w/ form
author: PipisCrew
date: 2015-03-04
categories: []
toc: true
---

reference 
[http://www.w3schools.com/php/php_file_upload.asp](http://www.w3schools.com/php/php_file_upload.asp)
browser compatibility problem - [http://portfolio.planetjon.ca/2014/01/26/submit-file-input-via-ajax-jquery-easy-way/](http://portfolio.planetjon.ca/2014/01/26/submit-file-input-via-ajax-jquery-easy-way/)
[http://www.w3.org/TR/html-markup/input.file.html](http://www.w3.org/TR/html-markup/input.file.html)

```js
//index.html

	//custom filesize validation
	function checkSize(max_size) {
	    var input = document.getElementById("cvfile");

	    if(input.files && input.files.length == 1)  {           
	        if (input.files[0].size > max_size) {
	            alert("The file must be less than " + (max_size/1024/1024) + "MB");
	            return false;
	        }
	    }

	    return true;
	}

<form name="cv" action="upload.php" method="post" enctype="multipart/form-data" onsubmit="return checkSize(2097152)">

	<input id='dob' name='dob' type="date" min='1979-01-01' max='1996-01-01' class='form-control' placeholder='dob' required="" autofocus="">
	<input id='city' name='city' type="text" class='form-control' placeholder='city' required="">
	<input id='telephone' name='telephone' type='tel' class='form-control' placeholder='tel' required="">
	<input id='portofolio' name='portofolio' type='url' class='form-control' placeholder='portofolio url'>
	<input class='form-control' type="file" name="cvfile" id="cvfile" size="40" accept="application/pdf,application/msword, application/vnd.ms-excel,application/vnd.ms-powerpoint,application/vnd.openxmlformats-officedocument.presentationml.slideshow,application/vnd.openxmlformats-officedocument.presentationml.presentation,,application/vnd.openxmlformats-officedocument.wordprocessingml.document , text/plain, application/pdf, image/*" required="">

	<button id="btn" class="btn btn-primary btn-large" type="submit" name="submit">
		Submit
	</button>

</form>
```

```js
//upload.php
<?php if="" (!isset($_post["dob"])="" ||="" !isset($_post["city"])="" ||="" !isset($_post["telephone"])="" ||="" !isset($_files["cvfile"])="" ||="" !isset($_post["portofolio"]))="" {="" die("error="" invalid="" input");="" }="" $target_dir="uploads/" ;="" $target_file="$target_dir" .="" basename($_files["cvfile"]["name"]);="" if="" (move_uploaded_file($_files["cvfile"]["tmp_name"],="" $target_file))="" {="" echo="" "the="" file="" ".="" basename(="" $_files["cvfile"]["name"]).="" "="" has="" been="" uploaded.";="" }="" else="" {="" echo="" "sorry,="" there="" was="" an="" error="" uploading="" your="" file.";="" }=""?>
```

* * *

when tried to serialize the form with jQuery, weird things happened, solution submit natural the form.

```js
//index.html

 	function submitform()
	{//when user press Check anchor
		//your custom code here, submit, without jQ help! Plain via form name! 
		document.cv.submit();
	}

    //custom filesize validation
    function checkSize(max_size) {
        var input = document.getElementById("cvfile");

        if(input.files && input.files.length == 1)  {
            if (input.files[0].size > max_size) {
                alert("The file must be less than " + (max_size/1024/1024) + "MB");
                return false;
            }
        }

        return true;
    }

<form name="cv" action="upload.php" method="post" enctype="multipart/form-data" onsubmit="return checkSize(2097152)">

    <input id='dob' name='dob' type="date" min='1979-01-01' max='1996-01-01' class='form-control' placeholder='dob' required="" autofocus="">
    <input id='city' name='city' type="text" class='form-control' placeholder='city' required="">
    <input id='telephone' name='telephone' type='tel' class='form-control' placeholder='tel' required="">
    <input id='portofolio' name='portofolio' type='url' class='form-control' placeholder='portofolio url'>
    <input class='form-control' type="file" name="cvfile" id="cvfile" size="40" accept="application/pdf,application/msword, application/vnd.ms-excel,application/vnd.ms-powerpoint,application/vnd.openxmlformats-officedocument.presentationml.slideshow,application/vnd.openxmlformats-officedocument.presentationml.presentation,,application/vnd.openxmlformats-officedocument.wordprocessingml.document , text/plain, application/pdf, image/*" required="">

[Check](javascript: submitform())

<!-- WARNING SHOULD NOT BE TYPE SUBMIT (OTHERWISE CONFLICT WITH THE JS CALL)
  		<button id="btn" class="btn btn-primary btn-large" type="submit" name="submit">
			Submit
		</button>-->

</form>
```

origin - http://www.pipiscrew.com/?p=2523 phpjs-submit-a-file-w-form