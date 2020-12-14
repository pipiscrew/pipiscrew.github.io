---
title: o[jQuery] Gritter
author: PipisCrew
date: 2014-11-05
categories: []
toc: true
---

A small growl-like notification plugin for jQuery

![](https://www.pipiscrew.com/wp-content/uploads/2014/11/snap145.png "snap145")

[http://github.com/jboesch/Gritter/](http://github.com/jboesch/Gritter/)

sample code :
```js
$.gritter.add({
	title: 'Contract Closed!',
	text: 'Client : PipisCrew  
click [here](http://google.com) to see client details',
	image: 'notify.png',
	sticky: true,
	before_open: function(e){
		this.oo= "test"; //store new property
	},
	before_close: function(e){
		console.log(this.oo); //read new property
	},
	after_close: function(e){
		console.log(this.oo); //read new property
	}
});
```

origin - http://www.pipiscrew.com/?p=1709 jquery-gritter