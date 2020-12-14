---
title: Form Submit Buttons That Go To Different URLs
author: PipisCrew
date: 2017-08-03
categories: [news]
toc: true
---

```js
<form name="form">

  <input type="submit" onclick="javascript: form.action='/submit';">
  <input type="submit" onclick="javascript: form.action='/submit-2';"> 

</form>	
```

```js
<form action="/submit">

  <input type="submit" value="Submit">

  <input type="submit" value="Go Elsewhere" formaction="/elsewhere">

</form>
```

src - https://css-tricks.com/separate-form-submit-buttons-go-different-urls/
https://www.w3schools.com/Tags/att_button_formaction.asp

origin - http://www.pipiscrew.com/?p=9622 form-submit-buttons-that-go-to-different-urls