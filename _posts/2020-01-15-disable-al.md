---
title: disable all contents of div
author: PipisCrew
date: 2020-01-15
categories: [js]
toc: true
---

```js
//https://stackoverflow.com/a/15555422
$('#age-group-column *').children().off('click');

--

//http://stackoverflow.com/questions/15555295/how-to-disable-div-element-and-everything-inside

$("#oCOMP_picUploadDIV *").prop("disabled", true).off('click');
```

origin - https://www.pipiscrew.com/?p=16564 disable-all-contents-of-div