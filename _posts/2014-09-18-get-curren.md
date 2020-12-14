---
title: Get Currency Exchange Rate
author: PipisCrew
date: 2014-09-18
categories: []
toc: true
---

```js
<?php
//http://www.ecb.int/stats/exchange/eurofxref/html/index.en.html
//the file is updated daily between 2.15 p.m. and 3.00 p.m. CET

$XMLContent=file("http://www.ecb.europa.eu/stats/eurofxref/eurofxref-daily.xml"); 
    foreach($XMLContent as $line){ 
        if(preg_match("/currency='([[:alpha:]]+)'/",$line,$currencyCode)){ 
            if(preg_match("/rate='([[:graph:]]+)'/",$line,$rate)){ 
                //Output the value of 1EUR for a currency code 
                echo'1€='.$rate[1].' '.$currencyCode[1].'  
'; 
            } 
        } 
} 
?>
```

origin - http://www.pipiscrew.com/?p=1326 php-get-currency-exchange-rate