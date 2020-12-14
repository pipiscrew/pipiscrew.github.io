---
title: double dollar
author: PipisCrew
date: 2015-07-24
categories: []
toc: true
---

reference :
[http://php.net/manual/en/language.variables.variable.php](http://php.net/manual/en/language.variables.variable.php)

![](https://www.pipiscrew.com/wp-content/uploads/2015/07/snap129.png "snap129")

Fig.1 - At start, we have a plain form with POST method and an element named <b style="color:red">newpass**.

```js
//test.php
<?php $blockkeys="array('_SERVER','_SESSION','_GET','_POST','_COOKIE','charset','ip','islinux','url','url_info','doc_root','fm_self','path_info');" foreach="" ($_post="" as="" $key=""?> $val) //LOOP through POST variables
    	if (array_search($key,$blockKeys) === false)
    		{
    			echo "{$key} - {$val}.  
";

    			$$key=$val;
    		}

    echo $newpass;

	echo "<form method='post'>";
	echo "<input type='text' name='newpass' placeholder='type a password' required="">  

";
	echo "<button type='submit'>Set Password</button>  
";
	echo "</form>"; 
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/07/snap1291.png "snap129")

Fig.2 - When submitted using the $$ (line 10) creates a variable <b style="color:red">newpass** (aka $key) and set the value submitted (aka $val).</b></b>

origin - http://www.pipiscrew.com/?p=3460 php-double-dollar