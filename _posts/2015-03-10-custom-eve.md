---
title: Custom Events in JavaScript
author: PipisCrew
date: 2015-03-10
categories: []
toc: true
---

[http://www.kirupa.com/html5/custom_events_js.htm](http://www.kirupa.com/html5/custom_events_js.htm)

```js
document.body.addEventListener("myEventName", doSomething, false);

function doSomething(e) {
    alert("Event is called: " + e.type);
}

var myEvent = new CustomEvent("myEventName");
dodocument.body.dispatchEvent(myEvent);
```

origin - http://www.pipiscrew.com/?p=2572 js-custom-events-in-javascript