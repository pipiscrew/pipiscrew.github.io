---
title: Whatever Origin
author: PipisCrew
date: 2016-06-23
categories: [js]
toc: true
---

A humble open source clone of [AnyOrigin](http://anyorigin.com/)

[http://www.whateverorigin.org/](http://www.whateverorigin.org/)

```js
//Usage is similar to anyorigin. For example, to fetch the data from http://google.com with jQuery, use this snippet:
$.getJSON('http://whateverorigin.org/get?url=' + encodeURIComponent('http://google.com') + '&callback=?', function(data){
	alert(data.contents);
});
```

```js
//advance example
jQuery.ajaxSetup({
    scriptCharset: "utf-8", //or "ISO-8859-1"
    contentType: "application/json; charset=utf-8"
});

jQuery(window).load(function() {
	var currentURL = window.location.href;
	if(currentURL.indexOf("/p/") > -1){
		jQuery.getJSON('http://whateverorigin.org/get?url=' + 
			encodeURIComponent(jQuery('.cart a').attr('href')) + '&callback=?',
			function (data) {

				//If the expected response is text/plain
				if(jQuery('.shop_attributes td').text().indexOf('8086') > -1){
					if(jQuery(data.contents).find('#tabs-1').text().trim() != '')
						jQuery("#section-description").html(jQuery(data.contents).find('#tabs-1'));
				}
				if(jQuery('.shop_attributes td').text().indexOf("amstrad") > -1){
					if(jQuery(data.contents).find('#long-description').text().trim() != '')
						jQuery("#section-description").html(jQuery(data.contents).find('#long-description'));
				}
				if(jQuery('.shop_attributes td').text().indexOf("amiga") > -1){
					if(jQuery(data.contents).find('#read-more').text().trim() != '')
						jQuery("#section-description").html(jQuery(data.contents).find('#read-more'));
				}
				//If the expected response is JSON
				//var response = $.parseJSON(data.contents);

		});
	}
});

```

origin - http://www.pipiscrew.com/?p=5886 whatever-origin