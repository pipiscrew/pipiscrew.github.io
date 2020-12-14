---
title: Reverse Engineering One Line of JavaScript
author: PipisCrew
date: 2017-07-23
categories: [js]
toc: true
---

https://www.alexkras.com/reverse-engineering-one-line-of-javascript/

https://codepen.io/akras14/pen/yXGzVd

author - http://www.p01.org/

```js

**Oringinal source is [here](http://www.p01.org/128b_raytraced_checkboard/) created by [p01](https://twitter.com/search?q=p01&src=typd).** You can see my attempt at reverse engineering it [here](https://www.alexkras.com/reverse-engineering-one-line-of-javascript/).

n=setInterval("for(n+=7,i=k,P='p.\\n';i-=1/k;P+=P[i%2?(i%2*j-j+n/k^j)&1:2])j=k/i;p.innerHTML=P",k=64)
    ```

origin - http://www.pipiscrew.com/?p=9276 reverse-engineering-one-line-of-javascript