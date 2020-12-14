---
title: o[html] submit form to new window
author: PipisCrew
date: 2015-07-21
categories: []
toc: true
---

You probably knew that you could force a link into opening a new tab or window with the target="_blank" attribute (deprecated, but universally still supported).

```js[link](#)```

But you can use the same exact attribute on forms to get the same result:

```js
<form action="x.php" method="post" target="_blank">
    ...
</form>
```

source - [https://css-tricks.com/snippets/html/form-submission-new-window/](https://css-tricks.com/snippets/html/form-submission-new-window/)

origin - http://www.pipiscrew.com/?p=3401 html-submit-form-to-new-window