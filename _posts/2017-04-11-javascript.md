---
title: JavaScript console tricks
author: PipisCrew
date: 2017-04-11
categories: [js]
toc: true
---

One other trick I found useful is the **console.table()** method. 

http://www.codediesel.com/javascript/javascript-console-tricks/

```js
var payments = [
{date: "2011-11-14T16:17:54Z", quantity: 2, total: 190, tip: 100, type: "tab"},
{date: "2011-11-14T16:20:19Z", quantity: 2, total: 190, tip: 100, type: "tab"},
{date: "2011-11-14T16:28:54Z", quantity: 1, total: 300, tip: 200, type: "visa"}];

console.table(payments);
```

dump any object
```js
//https://css-tricks.com/debugging-tips-tricks/
console.dir(document)
```

origin - http://www.pipiscrew.com/?p=7310 javascript-console-tricks