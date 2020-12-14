---
title: context menu
author: PipisCrew
date: 2016-03-26
categories: [js]
toc: true
---

[https://github.com/sydcanem/bootstrap-contextmenu](https://github.com/sydcanem/bootstrap-contextmenu)

[https://github.com/callmenick/Custom-Context-Menu](https://github.com/callmenick/Custom-Context-Menu)

* * *

## supports dynamic elements

[https://github.com/swisnl/jQuery-contextMenu](https://github.com/swisnl/jQuery-contextMenu)

```js
//http://swisnl.github.io/jQuery-contextMenu/demo/dynamic-create.html

$(function(){}

 $.contextMenu({
		selector: 'a', 
		build: function($trigger, e) {
		console.log($trigger.attr('href'));
		// this callback is executed every time the menu is to be shown
		// its results are destroyed every time the menu is hidden
		// e is the original contextmenu event, containing e.pageX and e.pageY (amongst other data)
			return {
				callback: function(key, options) {
					var m = "clicked: " + key;
					window.console && console.log(m) || alert(m); 
				},
				items: {
					"edit": {name: "Edit", icon: "edit"},
					"cut": {name: "Cut", icon: "cut"},
					"copy": {name: "Copy", icon: "copy"},
					"paste": {name: "Paste", icon: "paste"},
					"delete": {name: "Delete", icon: "delete"},
					"sep1": "---------",
					"quit": {name: "Quit", icon: function($element, key, item){ return 'context-menu-icon context-menu-icon-quit'; }}
				}
			};
		}
	});

});
```

* * *

## 2012 - 5 jQuery Right Click Context Menu Plugins

[http://www.sitepoint.com/right-click-context-menu-plugins/](http://www.sitepoint.com/right-click-context-menu-plugins/)

origin - http://www.pipiscrew.com/?p=4586 js-context-menu