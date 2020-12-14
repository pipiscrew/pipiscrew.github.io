---
title: o[bootstrap] typeahead
author: PipisCrew
date: 2020-01-23
categories: [js]
toc: true
---

plain **bootstrap v2.x**, combo autocomplete

With Twitter **bootstrap v3** the typeahead plugin **had been dropped**. @mdo says: "in favor of folks using Twitter's typeahead. Twitter's typeahead has more features than the old bootstrap-typeahead.js and less bugs." more [http://twitter.github.io/typeahead.js/](http://twitter.github.io/typeahead.js/)

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/Snap320.png "Snap320")

```js
<input type="text" class="form-control" id="test" placeholder="fullname">
```

```js
var search = $('input#test');

$(search).typeahead({
    source: [
        'Dave Mustaine',
        'Tom Morello',
        'Jim Root',
        'Kirk Hammett',
        'Joe Perry',
        'Jimi Hendrix',
        'Eric Clapton',
        'Billy Duffy',
        'Johnny Hickman',
        'Eddie Van Halen',
        'Dimebag Darrell',
        'Noel Gallagher'
    ],
    items: 5
});
```

* * *

fuck it, dont waste your time, use :
[https://github.com/bassjobsen/Bootstrap-3-Typeahead](https://github.com/bassjobsen/Bootstrap-3-Typeahead)

truly working.

```js
//https://github.com/bassjobsen/Bootstrap-3-Typeahead/issues/99#issuecomment-76320058
$('#search_box').typeahead({
    source: function (query, process) {
        return $.get("node_search.php?txt=" + query, function (data) {
        	console.log(data);
            return process(data);
        },'json');
    }
});
```

```js
//node_search.php
<?php require_once="" ('config.php');="" $db="connect_mysql();" $rows="getSet($db," select"="" node_id="" as="" id,="" node_title="" as="" name="" from="" nodes="" where="" node_body="" like="" concat('%',="" ,="" '%')="" or="" node_title="" like="" concat('%',="" ,="" '%')",array($_get['txt'],$_get['txt']));="" $r="array();" foreach($rows="" as="" $row)="" {="" $r[]="array(" id""="=""?"?> $row["id"], "name" => $row["name"]);
}

echo json_encode($r);
```

origin - http://www.pipiscrew.com/?p=1448 bootstrap-typehead