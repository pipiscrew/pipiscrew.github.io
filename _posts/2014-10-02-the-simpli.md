---
title: the simpliest upload/download
author: PipisCrew
date: 2014-10-02
categories: []
toc: true
---

**index.html**
```js
<form action="upload.php" method="POST" enctype="multipart/form-data">
    <input type="file" name="image">
    <input type="submit">
</form>

[Download](download.php?file=yourfilename.here)
```

**upload.php**
```js
<?php *="" *="" simple="" file="" upload="" system="" with="" php.="" *="" created="" by="" tech="" stream="" *="" original="" source="" at="" http://techstream.org/web-development/php/single-file-upload-with-php="" *="" this="" program="" is="" free="" software;="" you="" can="" redistribute="" it="" and/or="" modify="" *="" it="" under="" the="" terms="" of="" the="" gnu="" general="" public="" license="" as="" published="" by="" *="" the="" free="" software="" foundation;="" either="" version="" 2="" of="" the="" license,="" or="" *="" (at="" your="" option)="" any="" later="" version.="" *="" *="" this="" program="" is="" distributed="" in="" the="" hope="" that="" it="" will="" be="" useful,="" *="" but="" without="" any="" warranty;="" without="" even="" the="" implied="" warranty="" of="" *="" merchantability="" or="" fitness="" for="" a="" particular="" purpose.="" see="" the="" *="" gnu="" general="" public="" license="" for="" more="" details.="" *="" */="" if(isset($_files['image'])){="" $errors="array();" $file_name="$_FILES['image']['name'];" $file_size="$_FILES['image']['size'];" $file_tmp="$_FILES['image']['tmp_name'];" $file_type="$_FILES['image']['type'];" $file_ext="strtolower(end(explode('.',$_FILES['image']['name'])));" $expensions="array(" jpeg","jpg","png");"="" if(in_array($file_ext,$expensions)="==" false){="" $errors[]="extension not allowed, please choose a JPEG or PNG file." ;="" }="" if($file_size=""?> 2097152){
		$errors[]='File size must be excately 2 MB';
		}				
		if(empty($errors)==true){
			$t = getcwd();
			move_uploaded_file($file_tmp,$t."/images/".$file_name);
			echo "Success"."  
"; 
			echo "File Name :".$_FILES['image']['name']."  
"; 
			echo "File Size :".$_FILES['image']['size']."  
"; 
			echo "File Type :".$_FILES['image']['type']."  
"; 
			//echo "![](\"$path\")";
		}else{
			print_r($errors);
		}
	}
?>
```

**download.php**
```js
<?php $file="basename($_GET['file']);" $t="getcwd();" $file="$t" .="" '/images/'.$file;="" if(!$file){="" file="" does="" not="" exist="" die('file="" not="" found');="" }="" else="" {="" header("cache-control:="" public");="" header("content-description:="" file="" transfer");="" header("content-disposition:="" attachment;="" filename=".$_GET['file']);
    header(" content-type:="" application/zip");="" header("content-transfer-encoding:="" binary");="" read="" the="" file="" from="" disk="" readfile($file);="" }=""?>
```

the directory structure is :
index.html
\images\   <--here uploads_the="" dir_must_exists="" -="" set="" chmod="700" upload.php="" download.php="" -------------------="" easier="" with="" :="" http://hayageek.com/docs/jquery-upload-file.php="" ||="" https://github.com/hayageek/jquery-upload-file="" uploads_the="" dir_must_exists="" -="" set="" chmod="700" upload.php="" download.php="" -------------------="" easier="" with="" :="" http://hayageek.com/docs/jquery-upload-file.php="" ||=""></--here>

origin - http://www.pipiscrew.com/?p=1443 php-the-simpliest-uploaddownload