---
title: o[html] display facebook page in a div!?
author: PipisCrew
date: 2015-07-17
categories: []
toc: true
---

[http://developers.facebook.com/docs/plugins/page-plugin/](http://developers.facebook.com/docs/plugins/page-plugin/)

```js
<div id="fb-root"></div>
<div class="fb-page" data-href="https://www.facebook.com/durex" data-width="500" data-height="700" data-hide-cover="false" data-show-facepile="true" data-show-posts="true"></div>

	(function(d, s, id) {
	  var js, fjs = d.getElementsByTagName(s)[0];
	  if (d.getElementById(id)) return;
	  js = d.createElement(s); js.id = id;
	  js.src = "//connect.facebook.net/en_US/sdk.js#xfbml=1&version=v2.3";
	  fjs.parentNode.insertBefore(js, fjs);
	}(document, 'script', 'facebook-jssdk'));

```

origin - http://www.pipiscrew.com/?p=3326 html-display-facebook-page-in-a-div