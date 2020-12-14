---
title: Skeleton Grid System
author: PipisCrew
date: 2017-09-16
categories: [css]
toc: true
---

A dead simple, responsive boilerplate.

https://github.com/dhg/Skeleton

[http://getskeleton.com/](http://getskeleton.com/)

[http://thisisdallas.github.io/Simple-Grid/](http://thisisdallas.github.io/Simple-Grid/)

[http://purecss.io/grids/](http://purecss.io/grids/)

[https://css-tricks.com/dont-overthink-it-grids/](https://css-tricks.com/dont-overthink-it-grids/)

[http://960.gs/](http://960.gs/)

[https://css-tricks.com/dont-overthink-it-grids/](https://css-tricks.com/dont-overthink-it-grids/)

[http://www.cssgrid.co/](http://www.cssgrid.co/)

A grid system for humans [http://jeet.gs/](http://jeet.gs/)

The lightweight, responsive and modern CSS framework - [https://picturepan2.github.io/spectre/](https://picturepan2.github.io/spectre/)

[http://minicss.org/](http://minicss.org/)

```js
@charset "utf-8";
/* CSS Document */

body {
	margin:0px;
	padding:0px;
}
* {
	-webkit-box-sizing: border-box;
	-moz-box-sizing: border-box;
	box-sizing: border-box;
}
*:before, *:after {
	-webkit-box-sizing: border-box;
	-moz-box-sizing: border-box;
	box-sizing: border-box;
}
.container, .container-fluid {
	padding-right:15px;
	padding-left:15px;
	margin-right:auto;
	margin-left:auto;
}
.container {
	width:100%;
}
.container-fluid {
	width:100%;
}
.row {
	margin-right:-15px;
	margin-left:-15px;
}
.container:after, .container-fluid:after, .row:after {
	display:table;
	content:" ";
	clear:both;
}
div[class*="col-"],li[class*="col-"] {
	padding-right:15px;
	padding-left:15px;
	float:left;
}
/* EXTRA SMALL (Mobile Phones ETC) */
.col-xs-12 {
	width:100%
}
.col-xs-11 {
	width:91.66666667%
}
.col-xs-10 {
	width:83.33333333%
}
.col-xs-9 {
	width:75%
}
.col-xs-8 {
	width:66.66666667%
}
.col-xs-7 {
	width:58.33333333%
}
.col-xs-6 {
	width:50%
}
.col-xs-5 {
	width:41.66666667%
}
.col-xs-4 {
	width:33.33333333%
}
.col-xs-3 {
	width:25%
}
.col-xs-2 {
	width:16.66666667%
}
.col-xs-1 {
	width:8.33333333%
}
.col-xs-offset-12 {
	margin-left:100%
}
.col-xs-offset-11 {
	margin-left:91.66666667%
}
.col-xs-offset-10 {
	margin-left:83.33333333%
}
.col-xs-offset-9 {
	margin-left:75%
}
.col-xs-offset-8 {
	margin-left:66.66666667%
}
.col-xs-offset-7 {
	margin-left:58.33333333%
}
.col-xs-offset-6 {
	margin-left:50%
}
.col-xs-offset-5 {
	margin-left:41.66666667%
}
.col-xs-offset-4 {
	margin-left:33.33333333%
}
.col-xs-offset-3 {
	margin-left:25%
}
.col-xs-offset-2 {
	margin-left:16.66666667%
}
.col-xs-offset-1 {
	margin-left:8.33333333%
}
.col-xs-offset-0 {
	margin-left:0
}

/* SMALL (Tablets ETC) */
@media (min-width:768px) {
.col-sm-12 {
	width:100%
}
.col-sm-11 {
	width:91.66666667%
}
.col-sm-10 {
	width:83.33333333%
}
.col-sm-9 {
	width:75%
}
.col-sm-8 {
	width:66.66666667%
}
.col-sm-7 {
	width:58.33333333%
}
.col-sm-6 {
	width:50%
}
.col-sm-5 {
	width:41.66666667%
}
.col-sm-4 {
	width:33.33333333%
}
.col-sm-3 {
	width:25%
}
.col-sm-2 {
	width:16.66666667%
}
.col-sm-1 {
	width:8.33333333%
}
.col-sm-offset-12 {
	margin-left:100%
}
.col-sm-offset-11 {
	margin-left:91.66666667%
}
.col-sm-offset-10 {
	margin-left:83.33333333%
}
.col-sm-offset-9 {
	margin-left:75%
}
.col-sm-offset-8 {
	margin-left:66.66666667%
}
.col-sm-offset-7 {
	margin-left:58.33333333%
}
.col-sm-offset-6 {
	margin-left:50%
}
.col-sm-offset-5 {
	margin-left:41.66666667%
}
.col-sm-offset-4 {
	margin-left:33.33333333%
}
.col-sm-offset-3 {
	margin-left:25%
}
.col-sm-offset-2 {
	margin-left:16.66666667%
}
.col-sm-offset-1 {
	margin-left:8.33333333%
}
.col-sm-offset-0 {
	margin-left:0
}
}

/* MEDIUM (Small Desktops ETC) */
@media (min-width:992px) {
.col-md-12 {
	width:100%
}
.col-md-11 {
	width:91.66666667%
}
.col-md-10 {
	width:83.33333333%
}
.col-md-9 {
	width:75%
}
.col-md-8 {
	width:66.66666667%
}
.col-md-7 {
	width:58.33333333%
}
.col-md-6 {
	width:50%
}
.col-md-5 {
	width:41.66666667%
}
.col-md-4 {
	width:33.33333333%
}
.col-md-3 {
	width:25%
}
.col-md-2 {
	width:16.66666667%
}
.col-md-1 {
	width:8.33333333%
}
.col-md-offset-12 {
	margin-left:100%
}
.col-md-offset-11 {
	margin-left:91.66666667%
}
.col-md-offset-10 {
	margin-left:83.33333333%
}
.col-md-offset-9 {
	margin-left:75%
}
.col-md-offset-8 {
	margin-left:66.66666667%
}
.col-md-offset-7 {
	margin-left:58.33333333%
}
.col-md-offset-6 {
	margin-left:50%
}
.col-md-offset-5 {
	margin-left:41.66666667%
}
.col-md-offset-4 {
	margin-left:33.33333333%
}
.col-md-offset-3 {
	margin-left:25%
}
.col-md-offset-2 {
	margin-left:16.66666667%
}
.col-md-offset-1 {
	margin-left:8.33333333%
}
.col-md-offset-0 {
	margin-left:0
}
}

/* LARGE (Desktops) */
@media (min-width:1200px) {
.col-lg-12 {
	width:100%
}
.col-lg-11 {
	width:91.66666667%
}
.col-lg-10 {
	width:83.33333333%
}
.col-lg-9 {
	width:75%
}
.col-lg-8 {
	width:66.66666667%
}
.col-lg-7 {
	width:58.33333333%
}
.col-lg-6 {
	width:50%
}
.col-lg-5 {
	width:41.66666667%
}
.col-lg-4 {
	width:33.33333333%
}
.col-lg-3 {
	width:25%
}
.col-lg-2 {
	width:16.66666667%
}
.col-lg-1 {
	width:8.33333333%
}
.col-lg-offset-12 {
	margin-left:100%
}
.col-lg-offset-11 {
	margin-left:91.66666667%
}
.col-lg-offset-10 {
	margin-left:83.33333333%
}
.col-lg-offset-9 {
	margin-left:75%
}
.col-lg-offset-8 {
	margin-left:66.66666667%
}
.col-lg-offset-7 {
	margin-left:58.33333333%
}
.col-lg-offset-6 {
	margin-left:50%
}
.col-lg-offset-5 {
	margin-left:41.66666667%
}
.col-lg-offset-4 {
	margin-left:33.33333333%
}
.col-lg-offset-3 {
	margin-left:25%
}
.col-lg-offset-2 {
	margin-left:16.66666667%
}
.col-lg-offset-1 {
	margin-left:8.33333333%
}
.col-lg-offset-0 {
	margin-left:0
}
}

/*
sample :
<div class="container" id="contest">
  <div class="row">
    <div class="col-lg-12 col-md-12 col-sm-12 col-xs-12">
*/
```
#css #grid #col #row</div></div></div>

origin - http://www.pipiscrew.com/?p=2428 css-skeleton-grid-system