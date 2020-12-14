---
title: Adding custom php code as page template
author: PipisCrew
date: 2016-02-05
categories: [php,wordpress]
toc: true
---

source - [http://stackoverflow.com/a/2810723](http://stackoverflow.com/a/2810723)
[https://premium.wpmudev.org/blog/creating-custom-page-templates-in-wordpress/](https://premium.wpmudev.org/blog/creating-custom-page-templates-in-wordpress/)

under /wp-content/themes/themename/ make a new file templatename.php which is like 
```js
<?php *="" template="" name:="" templatename="" */=""?>
```

then when you go to 'add page', you will have an extra option to page attributes groupbox (template)
![snap096](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap096.png) 

if the pageattributes not appear, or the template you created is not there, go and change the wordpress theme to something else and restore it back to your custom. the page attributes will appear!

## Create a Login Widget With PHP Text Widget

http://www.satollo.net/plugins/php-text-widget
http://www.satollo.net/how-to-create-a-login-widget-with-php-text-widget

## Exec-PHP

https://wordpress.org/plugins/exec-php/

origin - http://www.pipiscrew.com/?p=3643 adding-custom-php-code-as-page-template