---
title: o[php+bootstrap] scan dir for picture files, present it via bootstrap thumbnail
author: PipisCrew
date: 2015-08-27
categories: [bootstrap,php]
toc: true
---

reference 
[http://getbootstrap.com/components/#thumbnails](http://getbootstrap.com/components/#thumbnails)
[http://stackoverflow.com/a/29948454](http://stackoverflow.com/a/29948454)

```js

function delete_image(e,fl){
	e.preventDefault();
    $.post("image_delete.php", {fl:fl}, function(data, status){
        alert(data + "\nPlease refresh the page");
    });
}

<div class="container">
	<div class="row">
<?php $img_dir='img/' ;="" image="" extensions="" $extensions="array('jpg'," 'jpeg',="" 'png',="" 'gif',="" 'bmp');="" init="" result="" $result="array();" directory="" to="" scan="" $directory="new" directoryiterator($img_dir);="" iterate="" foreach="" ($directory="" as="" $fileinfo)="" {="" must="" be="" a="" file="" if="" ($fileinfo-=""?>isFile()) {
	        // file extension
	        $extension = strtolower(pathinfo($fileinfo->getFilename(), PATHINFO_EXTENSION));
	        // check if extension match
	        if (in_array($extension, $extensions)) {
	            // add to result
	            $result[] = $fileinfo->getFilename();
	        }
	    }
	}

	 foreach($result as $fl)
	 {
	 	echo "	 		<div class='col-xs-2 col-sm-2 col-lg-2 col-md-2' style='margin-bottom:7px;'>
	 			[![]({$img_dir}{$fl})](#){$fl}  

	 			[Delete](#)
	 		 </div>\n";
	 }
?>

	</div>
</div>
```

```js
//image_delete.php
<?php @session_start();="" if="" (!isset($_session["id"])="" ||="" !isset($_post["fl"]))="" {="" header("location:="" index.php");="" exit="" ;="" }="" $fl="../img/" .$_post["fl"];="" try="" {="" if="" (file_exists($fl))="" {="" unlink($fl);="" echo="" "file="" deleted!";="" }="" else="" {="" echo="" "file="" doesnt="" exist!";="" }="" }="" catch(exception="" $e){="" echo="" 'caught="" exception:="" ',="" $e-=""?>getMessage(), "\n";
}

```

origin - http://www.pipiscrew.com/?p=1705 phpbootstrap-scan-dir-for-picture-files-present-it-via-bootstrap-thumbnail