---
title: o[css] bootstrap - glyphicon watermark in input
author: PipisCrew
date: 2015-06-11
categories: []
toc: true
---

source - [http://www.java2s.com/Tutorials/HTML_CSS/Bootstrap_Example/Form/Put_Glyphicon_Inside_Input_Box.htm](http://www.java2s.com/Tutorials/HTML_CSS/Bootstrap_Example/Form/Put_Glyphicon_Inside_Input_Box.htm)

![](https://www.pipiscrew.com/wp-content/uploads/2015/06/snap102.png "snap102")

```js
//test

	<style>
		.left-inner-addon {
		  position: relative;
		}

		.left-inner-addon input {
		  padding-left: 40px;
		}

		.left-inner-addon i {
		  position: absolute;
		  padding: 10px 12px;
		}
		.right-inner-addon {
		  position: relative;
		}

		.right-inner-addon input {
		  padding-right: 30px;
		}

		.right-inner-addon i {
		  position: absolute;
		  right: 0px;
		  padding: 10px 12px;
		}
	</style>

	<div class="form-group">
		<label class="control-label"><span class="icon-building"></span>Company Manager : </label>
  		<div class="left-inner-addon">
		<i class="icon-user">* <input type="text" class="form-control" placeholder="Manager">
		</i></div>
	</div>  

	<div class="form-group">
		<label class="control-label"><span class="icon-building"></span>Company Owner : </label>
		<div class="right-inner-addon ">
			<i class="icon-user">* <input type="search" class="form-control" placeholder="Owner">
		</i></div>
	</div> 
```

origin - http://www.pipiscrew.com/?p=3120 css-bootstrap-glyphicon-watermark-in-input