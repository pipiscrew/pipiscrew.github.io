---
title: o[nodeJS] using JQDeferred with firebase
author: PipisCrew
date: 2017-02-26
categories: [news]
toc: true
---

reference :
[https://npmjs.org/package/JQDeferred](https://npmjs.org/package/JQDeferred) 
```js
function getBIDS(NodeKey) {
	var def = Deferred();

	var read2DB = new Firebase("https://" + baseURL + "/BIDS");

	read2DB.child(NodeKey).once('value', function(snap) {
		def.resolve(snap);
	});

	return def.promise();
}

//callback
getBIDS("-JDQ0Ba4ZfC1CJxHduNZ").done(function(e){
	console.log(e.val().debugfield);
});
```

origin - http://www.pipiscrew.com/?p=707 nodejs-using-jqdeferred-with-firebase