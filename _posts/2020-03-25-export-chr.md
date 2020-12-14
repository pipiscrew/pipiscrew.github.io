---
title: Export Chrome bookmarks as text
author: PipisCrew
date: 2020-03-25
categories: [js]
toc: true
---

```js
//src - https://gist.github.com/bgrins/5700426
//add reference to jQuery lib with :
//

/*
Export bookmarks from Chrome as text.
Go to Bookmarks Manager->Organize->Export to HTML file. 
Then open that file, open console and run this command:
*/

[].map.call(document.querySelectorAll("dt a"), function(a) {
   return a.textContent + " - " + a.href
}).join("\n");
```

similar - python export with **jQueryUI Accordion** - https://github.com/TheInsomniac/browser-bookmarks

origin - http://www.pipiscrew.com/?p=13010 export-chrome-bookmarks-as-text