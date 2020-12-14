---
title: o[php+js] convert line breaks to br
author: PipisCrew
date: 2015-07-22
categories: []
toc: true
---

//http://stackoverflow.com/a/5049048
//http://php.net/manual/en/function.nl2br.php

when on html-textarea element is multiline
and save on dbase.. Afterwards when we like to display it on html area (convert \r or \n) to   

```jsnl2br("This\r\nis\n\ra\nstring\r");
```

//jQ flavor
//http://stackoverflow.com/a/2919363

```js
function nl2br (str, is_xhtml) {   
    var breakTag = (is_xhtml || typeof is_xhtml === 'undefined') ? '  
' : '  
';    
    return (str + '').replace(/([^>\r\n]?)(\r\n|\n\r|\r|\n)/g, '$1'+ breakTag +'$2');
}
```

origin - http://www.pipiscrew.com/?p=3430 phpjs-convert-line-breaks-to-br