---
title: bootstrap-tagsinput
author: PipisCrew
date: 2015-05-14
categories: []
toc: true
---

jQuery tags input plugin based on Twitter Bootstrap (v2.x / v3 compatible).

[http://github.com/TimSchlechter/bootstrap-tagsinput](http://github.com/TimSchlechter/bootstrap-tagsinput)

> Twitter's typeahead don't work direct with Bootstrap 3

**warning** for bootstrap v3 typeahead you have to use **bassjobsen/Bootstrap-3-Typeahead** 
[http://github.com/bassjobsen/Bootstrap-3-Typeahead](http://github.com/bassjobsen/Bootstrap-3-Typeahead)

ex.
-dont add the taginput markup
-use 
```js

$('[name=aud_countries]').tagsinput({
  typeahead: {
    source: ['Amsterdam', 'Washington', 'Sydney', 'Beijing', 'Cairo']
  },
  freeInput: true
});

<div class='form-group'>
	<label>Countries :</label>
	<input type="text" name='aud_countries' class='form-control'>
</div>
```

get tags :
```js//form serialized - ok
$('[name=ad_keywords]').val();```

set tags :
```js$('[name=ad_keywords]').tagsinput('add', 'Washington', 'Sydney', 'Beijing');```

fix width (to appear 100%) :
```js

<style>
.bootstrap-tagsinput {
  width: 100% !important;
}
</style>
```

remove tags (modal closed event) :
```js$('[name=ad_keywords]').tagsinput('removeAll');```

![](https://www.pipiscrew.com/wp-content/uploads/2015/03/snap564.png "snap564")

validate tags!
[http://formvalidation.io/examples/bootstrap-tagsinput/](http://formvalidation.io/examples/bootstrap-tagsinput/)

and **Bootstrap Multi Email**
[http://github.com/ThinkBigPartners/bootstrap-multiEmail](http://github.com/ThinkBigPartners/bootstrap-multiEmail)

alternative 
[http://aehlke.github.io/tag-it/](http://aehlke.github.io/tag-it/)
[http://github.com/maxwells/bootstrap-tags](http://github.com/maxwells/bootstrap-tags)

origin - http://www.pipiscrew.com/?p=2643 js-bootstrap-tagsinput