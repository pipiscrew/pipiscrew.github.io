---
title: o[cscart] using smarty block allows us to add custom javascript snippet into tpls
author: PipisCrew
date: 2020-04-28
categories: [js,php]
toc: true
---

source - [http://www.webdesignerforum.co.uk/](http://www.webdesignerforum.co.uk/topic/28819-cs-cart-how-to-add-additional-scripts-to-head-section/#entry361770)

tested on CSCART v4.3

go to **Design > Layouts**
![snap551](https://www.pipiscrew.com/wp-content/uploads/2015/12/snap551.png)

go to a group and **add block**
![snap552](https://www.pipiscrew.com/wp-content/uploads/2015/12/snap552.png)

on modal appear choose the type **HTML/Smarty**
![snap553](https://www.pipiscrew.com/wp-content/uploads/2015/12/snap553.png)

on content use the smarty tag <strong style="color:red">{literal}**. Using this tag the CSCART doesnt put CDATA in front script.... example :

```js
//test
{literal}

  $(function() {
     function test(){
          alert("this is a test which allows javascript on a block!");
     }
  })

{/literal}

<div>
     pipiscrew - cscart v4.3 - test
</div>
```

ofc you MUST clear the cache via >> Administration > Storage and choose the Clear Cache

### CS-Cart tuts: How to change copyright.tpl with "My Changes" addon

https://www.youtube.com/watch?v=cMA_Ji-0URI

### CS-Cart API Class

[https://github.com/drahosistvan/cscartapi](https://github.com/drahosistvan/cscartapi) - [reference](http://forum.cs-cart.com/topic/31597-api-helper-class-for-cs-cart-4-free/)</strong>

origin - http://www.pipiscrew.com/?p=2975 cscart-use-smarty-block-allows-us-to-add-custom-javascript-snippet-into-tpls