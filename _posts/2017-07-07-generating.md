---
title: Generating Unique ID using JavaScript
author: PipisCrew
date: 2017-07-07
categories: [js]
toc: true
---

Makes use to the ES6 for convenience, crypto API and a bit of clever logic. What has been done is, it returns v4 Unique Identifier UUID for the format  xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx  where each  x is replaced with a random Hexadecimal digit from 0 to f and y is being replaced by a random Hexadecimal digit ranging from 8 to b. As you can see while generating unique id, ES6 adds the syntactic sugar around the crypto API. 

```js
//src - http://thewebjuice.com/how-to-generate-unique-id-using-javascript/

function uuidv4() {
  return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
    (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
  )
}
```

origin - http://www.pipiscrew.com/2017/07/generating-unique-id-using-javascript/ generating-unique-id-using-javascript