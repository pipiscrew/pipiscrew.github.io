---
title: Introduction to Sets in JavaScript
author: PipisCrew
date: 2017-06-21
categories: [js]
toc: true
---

Sets are a new object type with ES6 (ES2015) that allow to create collections of **unique values**. The values in a set can be either simple primitives like strings or integers, but more complex object types like object literals or arrays can also be part of a set.

```js
let animals = new Set();

animals.add('1');
animals.add('2');
animals.add('3');
animals.add('4');
console.log(animals.size); // 4
animals.add('2');
console.log(animals.size); // 4
```

origin - http://www.pipiscrew.com/2017/06/introduction-to-sets-in-javascript/ introduction-to-sets-in-javascript