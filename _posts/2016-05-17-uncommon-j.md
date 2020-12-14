---
title: Uncommon jQuery Selectors
author: PipisCrew
date: 2016-05-17
categories: [js]
toc: true
---

ref - [http://code.tutsplus.com/tutorials/uncommon-jquery-selectors--cms-25812](http://code.tutsplus.com/tutorials/uncommon-jquery-selectors--cms-25812)
```js
$("section *")         // Selects all descendants
$("section > *")       // Selects all direct descendants
$("section > * > *")   // Selects all second level descendants
$("section > * > * a") // Selects 3rd level links
```

```js
$("section:contains('Lorem Ipsum')").each(function() {
  $(this).html(
      $(this).html().replace(/Lorem Ipsum/g, "<span class='match-o'>Lorem Ipsum</span>")
    );
});
```

```js

*   Pellentesque [habitant morbi](dummy.html) tristique senectus.

*   Pellentesque habitant morbi tristique senectus.
  (... more list elements here ...)

*   Pellentesque habitant morbi tristique senectus.

*   Pellentesque [habitant morbi](dummy.html) tristique senectus.

$("li:has(a)").each(function(index) {
  $(this).css("color", "crimson");
});
```

## Poor Mans jQuery

One of the functions on the ‘document’ object is the querySelectorAll function. This function brings a similar experience to vanilla JavaScript by taking selectors as a parameter.

```js
//http://www.timmykokke.com/2016/05/poor-mans-jquery/

	window.$ = function (selector) { return document.querySelectorAll(selector); };

	var button = $("#btn");
	button[0].innerText="popay";
	button[0].disabled = true;

	var div = $("#myDIV");
	console.log(div);

```

origin - http://www.pipiscrew.com/?p=5397 uncommon-jquery-selectors