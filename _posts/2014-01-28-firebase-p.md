---
title: o[firebase] push with priority
author: PipisCrew
date: 2014-01-28
categories: []
toc: true
---

**PHP** 

```js
var myObj = JSON.stringify({name: 'My Name', address: 'My Address', '.priority': 123});
$.post('http://demo.firebase.com/demo/testing.json', myObj);
```**javascript**

```js
	var add2DB = new Firebase(url);

	vat itemOBJ = {
		title : $('#oCATEGORY_name').val(),
		logo : $('#oCATEGORY_logo').val(),
		'.priority' : $('#oCATEGORY_date').val()
		}

	add2DB.push(itemOBJ)
```

origin - http://www.pipiscrew.com/?p=779 firebase-push-with-priority