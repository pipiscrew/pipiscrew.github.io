---
title: get portion of an image on the fly
author: PipisCrew
date: 2015-07-18
categories: []
toc: true
---

references
[http://webcheatsheet.com/php/dynamic_image_generation.php](http://webcheatsheet.com/php/dynamic_image_generation.php)
[http://gist.github.com/davejamesmiller/3236415](http://gist.github.com/davejamesmiller/3236415)

output #on the fly# no file created :
```js
<?php $file="$_GET['file'];" $original="assets/logo.png" ;="" $thumbwidth="200;" $thumbheight="200;" get="" the="" current="" size="" &="" file="" type="" list($width,="" $height,="" $type)="getimagesize($original);" load="" the="" image="" switch="" ($type)="" {="" case="" imagetype_gif:="" $image="imagecreatefromgif($original);" break;="" case="" imagetype_jpeg:="" $image="imagecreatefromjpeg($original);" break;="" case="" imagetype_png:="" $image="imagecreatefrompng($original);" break;="" default:="" die("invalid="" image="" type="" (#{$type}=" . image_type_to_extension($type) . " )");="" }="" calculate="" height="" automatically="" if="" not="" given="" if="" ($thumbheight="==" null)="" {="" $thumbheight="round($height" *="" $thumbwidth="" $width);="" }="" ratio="" to="" resize="" by="" $widthproportion="$thumbWidth" $width;="" $heightproportion="$thumbHeight" $height;="" $proportion="max($widthProportion," $heightproportion);="" area="" of="" original="" image="" that="" will="" be="" used="" $origwidth="floor($thumbWidth" $proportion);="" $origheight="floor($thumbHeight" $proportion);="" co-ordinates="" of="" original="" image="" to="" use="" $x1="floor($width" -="" $origwidth)="" 2;="" $y1="floor($height" -="" $origheight)="" 2;="" resize="" the="" image="" $thumbimage="imagecreatetruecolor($thumbWidth," $thumbheight);="" imagecopyresampled($thumbimage,="" $image,="" 0,="" 0,="" $x1,="" $y1,="" $thumbwidth,="" $thumbheight,="" $origwidth,="" $origheight);="" tell="" the="" browser="" what="" kind="" of="" file="" is="" come="" in="" header("content-type:="" image/jpeg");="" output="" the="" newly="" created="" image="" in="" jpeg="" format="" imagejpeg($thumbimage);="" close="" the="" files="" imagedestroy($image);="" imagedestroy($thumbimage);="" ```=""  =""?>

## create thumb on disk (dirty code)

:)
```js
<?php $file="$_GET['file'];" resize_image($file);="" function="" resize_image($id)="" {="" $original="prod_img/{$id}.jpg" ;="" $target="prod_img/{$id}_thumb.jpg" ;="" if="" (file_exists($target))="" return="" $target;="" if="" (!file_exists($original))="" return="" "prod_img/404.jpg";="" $thumbwidth="200;" $thumbheight="200;" get="" the="" current="" size="" &="" file="" type="" list($width,="" $height,="" $type)="getimagesize($original);" load="" the="" image="" switch="" ($type)="" {="" case="" imagetype_gif:="" $image="imagecreatefromgif($original);" break;="" case="" imagetype_jpeg:="" $image="imagecreatefromjpeg($original);" break;="" case="" imagetype_png:="" $image="imagecreatefrompng($original);" break;="" default:="" die("invalid="" image="" type="" (#{$type}=" . image_type_to_extension($type) . " )");="" }="" calculate="" height="" automatically="" if="" not="" given="" if="" ($thumbheight="==" null)="" {="" $thumbheight="round($height" *="" $thumbwidth="" $width);="" }="" ratio="" to="" resize="" by="" $widthproportion="$thumbWidth" $width;="" $heightproportion="$thumbHeight" $height;="" $proportion="max($widthProportion," $heightproportion);="" area="" of="" original="" image="" that="" will="" be="" used="" $origwidth="floor($thumbWidth" $proportion);="" $origheight="floor($thumbHeight" $proportion);="" co-ordinates="" of="" original="" image="" to="" use="" $x1="floor($width" -="" $origwidth)="" 2;="" $y1="floor($height" -="" $origheight)="" 2;="" resize="" the="" image="" $thumbimage="imagecreatetruecolor($thumbWidth," $thumbheight);="" imagecopyresampled($thumbimage,="" $image,="" 0,="" 0,="" $x1,="" $y1,="" $thumbwidth,="" $thumbheight,="" $origwidth,="" $origheight);="" save="" the="" new="" image="" switch="" ($type)="" {="" case="" imagetype_gif:="" imagegif($thumbimage,="" $target);="" break;="" case="" imagetype_jpeg:="" imagejpeg($thumbimage,="" $target,="" 90);="" break;="" case="" imagetype_png:="" imagepng($thumbimage,="" $target);="" break;="" default:="" throw="" new="" logicexception;="" }="" tell="" the="" browser="" what="" kind="" of="" file="" is="" come="" in="" header("content-type:="" image/jpeg");="" output="" the="" newly="" created="" image="" in="" jpeg="" format="" imagejpeg($thumbimage);="" close="" the="" files="" imagedestroy($image);="" imagedestroy($thumbimage);="" return="" $target;="" }="" ```=""  =""  =""?>

## Facebook Open Graph No Image First Time

[http://stackoverflow.com/a/27913458/1320686](http://stackoverflow.com/a/27913458/1320686)

origin - http://www.pipiscrew.com/?p=3370 php-get-portion-of-an-image