---
title: Debug javascript tips
author: PipisCrew
date: 2019-07-17
categories: [js,angular]
toc: true
---

The **debugger statement** invokes any available debugging functionality, such as setting a breakpoint. If no debugging functionality is available (aka F12), this statement has no effect.

```js
//https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/debugger
function potentiallyBuggyCode() {
    debugger;

    if (this.User == null)
    .
    .
    .
}
```

## Debug Typescript into VSCode

[https://code.visualstudio.com/docs/typescript/typescript-debugging](https://code.visualstudio.com/docs/typescript/typescript-debugging)

## nodeJS remote debugging

```js
//src - https://github.com/nodejs/node/issues/23693

navigate @:
chrome://inspect/#devices

Open dedicated DevTools for Node
```

## webpack - casual by F12

![](https://i.imgur.com/xnpBy2q.png)

Dont forget, when replacing **functions** with **arrow functions** expression (also known as fat arrow function) can access **this**!!

origin - https://www.pipiscrew.com/?p=15101 debug-javascript-tips