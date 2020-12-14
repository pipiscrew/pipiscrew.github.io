---
title: o[html] Print CSS background
author: PipisCrew
date: 2015-04-30
categories: []
toc: true
---

example when :
```js
<div style="margin:0 0;padding:0 0;background:#2ea3fb;">
</div>
```

in browser appears a blue rectangle, when try to print the page this blue rectangle is not printed.

printed when :
```js
<div style="-webkit-print-color-adjust:exact; margin:0 0;padding:0 0;background:#2ea3fb;">
</div>
```

* * *

In chrome (newer versions 17+ I think), this is controlled by a CSS property on the items which developers can add :

```js
-webkit-print-color-adjust:exact;
```

source : [http://stackoverflow.com/a/9339257](http://stackoverflow.com/a/9339257)

* * *

```js
/*http://stackoverflow.com/a/12773239
However in general, print styles are either set using a media tag in your existing stylesheet:*/

@media print{
    /*styles here*/
}

/*or linking to a stylesheet specifically for print purposes:*/

```

similar - dont waste paper
```js
/*!
 * print.css v1.0.0
 * http://printstylesheet.com/
 *
 * Copyright (c) 2011 David Bushell
 * Dual licensed under the BSD or MIT licenses: http://printstylesheet.com/license.txt

 * Author: David Bushell
 * http://dbushell.com/
 */

/* use a media query to limit the CSS to only print devices, like a printer */
@media only print
{
	/* hide every element within the body */
	body * { display: none !important; }
	/* add a friendy reminder not to waste paper after the body */
	body:after { content: "Don't waste paper!"; }
}
```

* * *

so here I have a page with a bootstrap print button, where I like when clicked button will not printed
```js
<style type="text/css">
@media print {
    #btn_print {
        display: none;
    }
}
</style>

[Print]()
this is a test

```

origin - http://www.pipiscrew.com/?p=1985 html-print-css-background