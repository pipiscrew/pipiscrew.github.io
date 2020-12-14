---
title: jQuery functions
author: PipisCrew
date: 2015-11-10
categories: [js]
toc: true
---

![snap250](https://www.pipiscrew.com/wp-content/uploads/2015/11/snap250.png)

```js

var TheFramework = function () {
	var test1="alcohol";
	var test2;

    var myBoatUnderTheBridge = function () {
           console.log("myBoatUnderTheBridge -- " + test1);
    }

	return {
		CustomMethod: function (the_name) {
			console.log(test1);
			test1 = "cool";
			myBoatUnderTheBridge();
			console.log("method2"+the_name);
		},

		MyMethod: function () {
			console.log("method1");
		},

		MyMethod_with_RET: function () {
			console.log("method3");
			return ("this is came by MyMethod_with_RET");
		}
	}
}();

var myWork =  {
		MySampleMethod: function () {
			console.log("init2");
		}
}

TheFramework.MyMethod();

myWork.MySampleMethod();

TheFramework.CustomMethod("THIS IS A TEST");

console.log(TheFramework.MyMethod_with_RET());

console.log(TheFramework);

console.log(myWork);

```

* * *

> there is no class.create() in jquery, instead use regular JS to code the object up.
> create a class with associated object and then use $.extend() to work with the object.

```js
//https://forum.jquery.com/topic/creating-a-class-object-with-jquery
//http://api.jquery.com/jQuery.extend/
var Circle = function(x, y, r) {
      this.x = x;
      this.y = y;
      this.r = r;
}

$.extend(Circle.prototype, {
      area: function() {
            return Math.PI * this.r * this.r;
      },
      diameter: function() {
            return 2 * this.r;
      }
});
```

* * *

## jQuery

```js
//https://flydillonfly.wordpress.com/2011/05/06/writing-oo-javascript-using-jquery/

	$(function() {

		// create document
		APP.pageHelper = new APP.PageHelper();
		// need to call init manually with jQuery
		APP.pageHelper.initialize();

	});

	// namespace our code
	window.APP = {};

	// my class (no Class.create in JQuery so code in native JS)
	APP.PageHelper = function() {};

	// add functions to the prototype
	APP.PageHelper.prototype = {

	  // automatically called
	  initialize: function(name, sound) {
		this.myValue = "Foo";
		console.log(this.myValue);

		// attach event handlers, binding to 'this' object
		$("#myButton").click($.proxy(this.displayMessage, this));

	  },

	  displayMessage: function() {
		console.log("My value: " + this.myValue); // 'this' is the object not the clicked button!
	  }

	};

	<button id="myButton">Test</button>

```

* * *

## Pure JS

```js

	function Animal(name, sound) {
	  this.name = name;
	  this.sound = sound;
	}

	Animal.prototype.speak = function() {
	  result = (this.name + " says: " + this.sound + "!");
	  console.log(result);
	}

	var cat = new Animal('Kitty', 'Meow');
	cat.speak();

```

## A Simple, Powerful, Lightweight Class for jQuery by Justin Meyer

[http://blog.bitovi.com/a-simple-powerful-lightweight-class-for-jquery/](http://blog.bitovi.com/a-simple-powerful-lightweight-class-for-jquery/)

origin - http://www.pipiscrew.com/?p=2383 jquery-functions