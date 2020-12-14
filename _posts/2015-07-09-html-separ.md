---
title: o[html] separator into select
author: PipisCrew
date: 2015-07-09
categories: []
toc: true
---

source [http://stackoverflow.com/a/15816867](http://stackoverflow.com/a/15816867)
use em dash "—". It has no visible spaces between each character.

```js
<select name="pipiscrew_test_no_css_needed">
    <option val="a">A
    <option disabled="">————————
    <option val="b">B
</select>
```

test:
<select name="pipiscrew_test_no_css_needed">
    <option val="a">A
    <option disabled="">————————
    <option val="b">B
</select>

origin - http://www.pipiscrew.com/?p=3298 html-separator-into-select