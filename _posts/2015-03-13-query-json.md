---
title: query json file
author: PipisCrew
date: 2015-03-13
categories: []
toc: true
---

Query, manipulate and manage JSON data effortlessly.
[http://danski.github.io/spahql/](http://danski.github.io/spahql/)

* * *

Retrieves values from JSON objects for data binding (+nodeJS)
[http://github.com/mmckegg/json-query](http://github.com/mmckegg/json-query)

* * *

2007 

reference
[http://orangevolt.blogspot.gr/2012/12/8-ways-to-query-json-structures.html](http://orangevolt.blogspot.gr/2012/12/8-ways-to-query-json-structures.html)

homepage - [http://www.trentrichardson.com/jsonsql/](http://www.trentrichardson.com/jsonsql/)

```js

//button click
$('#btn').on('click', function(e) {
	$.getJSON("gfonts.json", function(json){

		dump(jsonsql.query("select * from json where (items.table=='wood') ",json));

	});
});
```

origin - http://www.pipiscrew.com/?p=2630 js-query-json-file