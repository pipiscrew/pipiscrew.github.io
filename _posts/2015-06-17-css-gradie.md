---
title: o[css] gradient
author: PipisCrew
date: 2015-06-17
categories: []
toc: true
---

[http://www.colorzilla.com/gradient-editor/](http://www.colorzilla.com/gradient-editor/)
or
[http://www.cssmatic.com](http://www.cssmatic.com)

```js
//html and body to height: 100% doesn't seem to work if the content needs to scroll.
//warning when make gradient and the page is scrollable gradient fucked up, simple add fixed at the end of each line.
//http://stackoverflow.com/a/3294418
background: -webkit-gradient(linear, left top, left bottom, from(#fff), to(#cbccc8)) fixed;

//for mobiles needs also 
 	html {
     height: auto;
     min-height: 100%;
  	}
```

origin - http://www.pipiscrew.com/?p=3162 css-gradient