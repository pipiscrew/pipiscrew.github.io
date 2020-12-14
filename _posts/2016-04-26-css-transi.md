---
title: o[css] transition all
author: PipisCrew
date: 2016-04-26
categories: [css]
toc: true
---

ref - [https://css-tricks.com/almanac/properties/t/transition/](https://css-tricks.com/almanac/properties/t/transition/)

```js
<style>
.testArea {
	height: 120px;
	float: left;
	padding: 10px 10px 0 10px;
	background: #ebebeb;
	margin-right: 20px;
	position: relative;
	transition: all .2s;
	margin-top: 10px;
}

.testArea:hover {
	cursor: pointer;
	background: #c4c3c3 !important;
}
</style>

<div class="testArea">
</div>
```

origin - http://www.pipiscrew.com/?p=5105 css-transition-all