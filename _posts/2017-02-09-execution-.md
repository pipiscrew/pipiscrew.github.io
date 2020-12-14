---
title: execution time calculation
author: PipisCrew
date: 2017-02-09
categories: [php]
toc: true
---

```js
//src - http://stackoverflow.com/a/18336968

//place this before any script you want to calculate time
$time_start = microtime(true);

// do something

// Display Script End time
$time_end = microtime(true);

//dividing with 60 will give the execution time in minutes other wise seconds
$execution_time = ($time_end - $time_start)/60;

//execution time of the script
echo '**Total Execution Time:** '.$execution_time.' Mins';
```

origin - http://www.pipiscrew.com/?p=6670 php-execution-time-calculation