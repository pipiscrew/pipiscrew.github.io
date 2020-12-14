---
title: Exploring nodeJS Internals
author: PipisCrew
date: 2020-04-23
categories: [js]
toc: true
---

**V8** is the name of the JavaScript <span style="color: #3366ff;">engine that powers Google Chrome</span>. It's the thing that takes our JavaScript and executes it while browsing with Chrome.

V8 provides the runtime environment in which JavaScript executes. The DOM, and the other Web Platform APIs are provided by the browser.

The cool thing is that the JavaScript engine is independent of the browser in which it's hosted. This key feature enabled the rise of Node.js. **V8** was chosen to be the engine that powered Node.js back in **2009**, and as the popularity of Node.js exploded, **V8** became the engine that now powers an incredible amount of server-side code written in JavaScript. [src](https://nodejs.dev/the-v8-javascript-engine)

**Libuv** is an open-source library that handles the **thread-pool**, doing signaling, inter process communications all other magic needed to make the **asynchronous** tasks work at all. Libuv was originally developed for Node.js itself as an <span style="color: #3366ff;">abstraction</span> around [libev](http://software.schmorp.de/pkg/libev.html) (written in C).

> nodeJS is the glue that holds the two libraries together, thereby becoming a unique solution

https://www.smashingmagazine.com/2020/04/nodejs-internals/

#require #fs

origin - https://www.pipiscrew.com/?p=18326 exploring-nodejs-internals