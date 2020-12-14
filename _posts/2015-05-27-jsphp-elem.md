---
title: o[js+php] elementary - ajax json, php call
author: PipisCrew
date: 2015-05-27
categories: []
toc: true
---

indicators - [http://zanstra.home.xs4all.nl/picks/progress.html](http://zanstra.home.xs4all.nl/picks/progress.html)

I have an inputbox when it length is > 9 needed to validate for double record.. 

the input element
```js
<div class='form-group'>
	<label>Telephone :</label>![](img/mini_indicator.gif)
	<input name='telephone' class='form-control' placeholder='Telephone'>
</div>
```

```js
		$('[name=telephone]').on('input',function(e){
			if ($(this).val().length>9)
			{
			 	$("#tel_indicator").show();

					$.ajax({
						url : 'tab_leads_details_ask_4_double.php',
						dataType : 'json',
						type : 'POST',
						data : {
							"tel" : $(this).val()
						},
			            success : function(data) {
			            	$("#tel_indicator").hide();

			            	if (data=="error")
			            		alert("Error - when checking for double records via telephone");
			            	else if (data.rec_count>0)
			            	{
								$("[name=telephone]").css({ 'background': 'rgba(255, 0, 0, 0.3)' });
							}
							else 
								$("[name=telephone]").css({ 'background': 'white' });
						}
					});
			}
			else 
				$("[name=telephone]").css({ 'background': 'white' });
		});
```

```js
//tab_leads_details_ask_4_double.php
<?php require_once="" ('config.php');="" if(!isset($_post["tel"])){="" echo="" json_encode("error");="" return;="" }="" $db="connect();" $r="getScalar($db," select"="" count(client_id)="" from="" clients="" where="" telephone="?" ,array($_post["tel"]));"="" echo="" json_encode(array("rec_count"=""?>$r));

?>
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/03/snap5411.png "snap541")

1-length = 9
2-length = 10 -> ajax call php
3-php returns > 0

origin - http://www.pipiscrew.com/?p=2575 js-elementary-ajax-json-php-call