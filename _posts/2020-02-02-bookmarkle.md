---
title: Bookmarklet - List all links
author: PipisCrew
date: 2020-02-02
categories: [js]
toc: true
---

src - http://subsimple.com/bookmarklets/index.php

```js
javascript:if(frames.length>1)alert('Sorry, frames detected.');else{var wnd=open('','lnkswnd','width=400,height=500,top=0,left=0,scrollbars,resizable');var lnks=document.links;with(wnd.document){var s='<base target="_blank">';for(var i=0;i<><li>[<span onclick="window.close()">'+lnks[i].text+'</span>](+lnks[i].href+)</li>';}s+='';writeln(s);void(close());}}
```

* * *

bookmarklet list links to a target element

```js
var imgs = JSON.parse(document.getElementsByTagName("script")[37].innerText).image;imgs.forEach(e => {document.getElementsByClassName('page-title')[1].innerHTML=e;})
```

beautified :
```js
var imgs = JSON.parse(document.getElementsByTagName("script")[37].innerText).image;
document.getElementsByClassName('page-title')[1].innerHTML = '';
imgs.forEach(e => {
    document.getElementsByClassName('page-title')[1].innerHTML = document.getElementsByClassName('page-title')[1].innerHTML + "  
[image](" + e + ")";
})
```

origin - http://www.pipiscrew.com/?p=13174 bookmarklet-list-all-links