---
title: o[firebase] get unique nodeID
author: PipisCrew
date: 2017-02-26
categories: [news]
toc: true
---

```js
			function getNewNodeKey(url) {
				var getNewKey4DB = new Firebase(url);
				var ret = "";

				$.when(getNewKey4DB.push().name()).done(function(x) {
					ret = x;
				});

				return ret;
			}
```

The id is unique across all paths; it doesn’t matter which path you request it for.</pre>

origin - http://www.pipiscrew.com/?p=714 firebase-get-unique-nodeid