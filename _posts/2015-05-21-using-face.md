---
title: using facebook Graph API
author: PipisCrew
date: 2015-05-21
categories: []
toc: true
---

get page profile information with plain JS and FB graph

```js
//testarea

	<title>
			PipisCrew - Testarea
	</title>

		$(function()
			{

				$.get( "http://graph.facebook.com/cocacola", function( data ) {
					  var x;

					  x = "Category : " + data.category;

					  var likes = parseInt(data.likes);
					  x += "  
Likes : " + likes;

					  var tat = parseInt(data.talking_about_count);
					  x += "  
TAT : " + tat;

					  var res =  (tat/likes) * 100;					  
					  x += "  
Engagement Rate : " + parseFloat(res).toFixed(2);

					  $("#result").html(x);
				}).fail(function() {
					  alert('please check the Facebook handle'); 
				});

			});

		<div id="result">
		</div>

```

FYI the data object returned :
![](https://www.pipiscrew.com/wp-content/uploads/2015/05/snap039.png "snap039")

origin - http://www.pipiscrew.com/?p=3026 js-using-facebook-graph-api