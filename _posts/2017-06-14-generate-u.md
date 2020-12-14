---
title: Generate UUIDs in PHP
author: PipisCrew
date: 2017-06-14
categories: [php]
toc: true
---

```js
//src - https://rogerstringer.com/2013/11/15/generate-uuids-php/

<?php
function generate_uuid() {
	return sprintf( '%04x%04x-%04x-%04x-%04x-%04x%04x%04x',
		mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff ),
		mt_rand( 0, 0xffff ),
		mt_rand( 0, 0x0fff ) | 0x4000,
		mt_rand( 0, 0x3fff ) | 0x8000,
		mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff ), mt_rand( 0, 0xffff )
	);
}
?>
```

origin - http://www.pipiscrew.com/?p=8477 generate-uuids-in-php