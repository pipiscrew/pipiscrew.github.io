---
title: chrome bookmarks lightweight export
author: PipisCrew
date: 2018-09-23
categories: [app]
toc: true
---

today I exported chrome bookmarks from via :

Bookmark manager > Organize > Export to HTML

got **299kb** HTML file, what the heck? aha, embed the favicon as blob. my ass. 

-fire up notepad++
-CTRL+H
-make sure the RegEx is checked
-first Replace
```js
Find :
ICON=".*?">

Replace :
>
```
-second
```js
Find :
ADD_DATE=".*?"

Replace : null
```
-on the top of HTML add (to open the links to new page)
```js<base target="_blank">```

now enjoying a **29kb** HTML, cute!?

origin - https://www.pipiscrew.com/?p=14306 chrome-bookmarks-lightweight-export