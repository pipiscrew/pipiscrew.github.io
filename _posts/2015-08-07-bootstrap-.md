---
title: o[bootstrap] carousel (slide and refresh html details)
author: PipisCrew
date: 2015-08-07
categories: [js,css,bootstrap,php]
toc: true
---

```js
//http://stackoverflow.com/a/29671410/1320686
On Slide before
h('#HomeSlider').bind('slide.bs.carousel', function (e) {
   alert(h('#HomeSlider .item.active').html());
});

On Slide After
h('#HomeSlider').on('slid.bs.carousel', function (e) {
   alert(h('#HomeSlider .item.active').html());
});

```

ref - [http://stackoverflow.com/a/17841504/1320686](http://stackoverflow.com/a/17841504/1320686)

* * *

warning you have to use **carousel-inner** otherwise will not fire the event @ jQ!
so I end up with 
```js
//test.php
<?php $photo_detail="array();" $photo_name="array();" $photo_speciality="array();" .="" .="" fill="" the="" arrays="" by="" dbase="" +="" create="" slide="" elements="" (depend="" on="" records!)="" $i="0;" foreach($sc="" as="" $row)="" {="" $carousel_img="" .="	<pipiscrew  data-id='{$row[" member_id"]}'="" class='item".($i==0?" active":"")."'?>
			![](soccer_img/{$row["member_id"]}.jpg)
		";

		$photo_detail[]= $row["story"];
		$photo_name[] = $row["fullname"];
		$photo_speciality[] =$row["specialization"];

		$i+=1;
	}
?>
```

```js
$(function() {

	//convert PHP arrays to JS arrays via JSON
	var photo_detail = <?php echo="" json_encode($photo_detail);=""?>;
	var photo_name = <?php echo="" json_encode($photo_name);=""?>;
	var photo_speciality = <?php echo="" json_encode($photo_speciality);=""?>;

	//init slider with array[0] items
	$("#prem_detail").html(photo_detail[0]);
	$("#prem_name").html(photo_name[0]);
	$("#prem_speciality").html(photo_speciality[0]);

        //init the carousel
	$('#carousel_premium').carousel({
   		 interval: 5000
	});

	//using the 'slide after' event
	$('#carousel_premium').bind('slid.bs.carousel', function (e) {

		    var currentIndex = $('pipiscrew.active').index();

		    var items = $(this).children('.carousel-inner');

		    var x =0;

			//refresh the info, for current slide!
			$("#prem_detail").html(photo_detail[currentIndex]);
			$("#prem_name").html(photo_name[currentIndex]);
			$("#prem_speciality").html(photo_speciality[currentIndex]);

//find via data-id attribute (use : for dynamic dbase parse via dbase-ID + ajax)- tested&working 
//		    $('#carousel_premium .carousel-inner pipiscrew').each(function(i){
//
//		        if (x==currentIndex)
//		        {
//		        	
//		            console.log($(this).data('id'));
//		            return false;
//		        }
//		        
//		        x+=1;
//		            
//		    });
	});

}) //jQ ends

	<div class="row" style="border-top:1px #ffffff solid">
		<div class="col-xs-6 col-sm-6 col-lg-6 col-md-6">
			<div id="carousel_premium" class="carousel slide">
				<div class="carousel-inner">
<?=$carousel_img;???>
				</div>
			</div>
		</div>

		<div class="col-xs-6 col-sm-6 col-lg-6 col-md-6" style="margin-top: 5px">
			<span id="prem_name"></span> 

##### 

			<div id="prem_detail"></div>  
 [MORE INFO](https://pipiscrew.com)
		</div>
	</div>
```

![snap148](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap148.png)

origin - http://www.pipiscrew.com/?p=1431 bootstrap-carousel