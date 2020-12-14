---
title: justGage w Raphael reference
author: PipisCrew
date: 2017-06-06
categories: [js]
toc: true
---

reference
[http://justgage.com](http://justgage.com/)
[http://raphaeljs.com](http://raphaeljs.com/)

```js

      var g1;

      window.onload = function(){
		  var g1 = new JustGage({
			id: "g1", 
			value: 350, 
			min: 0,
			max: 600,
			title: "Test",
			label: "",    

		  });
		}

      //where somewhere later use as :
      g1.refresh(101);

      //more later change value with :
      $('#speedometer').val(100).change()

<div id="g1"></div>
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap090.png "snap090")

origin - http://www.pipiscrew.com/?p=1557 javascript-justgage-w-raphael-reference