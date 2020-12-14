---
title: Convert to Datetime MM/dd/yyyy HH-mm-ss
author: PipisCrew
date: 2017-07-20
categories: [sql]
toc: true
---

```js
//https://stackoverflow.com/a/19409616/1320686

//SQL Server 2005 and Onwards
SELECT CONVERT(VARCHAR(10), GETDATE(), 101) 
                        + ' ' + CONVERT(VARCHAR(8), GETDATE(), 108)
//SQL Server 2012 and later versions
SELECT FORMAT(GETDATE() , 'MM/dd/yyyy HH:mm:ss')
```

have in mind that in PHP slash & dash drives to different format
```js
//in general knows because or separator character
//http://php.net/manual/en/function.strtotime.php#91165
mm/dd/yyyy - 02/01/2003  - strtotime() returns : 1st February 2003
mm/dd/yy   - 02/01/03    - strtotime() returns : 1st February 2003
yyyy/mm/dd  - 2003/02/01 - strtotime() returns : 1st February 2003
dd-mm-yyyy - 01-02-2003  - strtotime() returns : 1st February 2003
yy-mm-dd   - 03-02-01    - strtotime() returns : 1st February 2003
```

MySQL & SQLServer represents the datetime field as :
```js
2015-09-29 17:47:28
```

origin - http://www.pipiscrew.com/?p=9230 convert-to-datetime-mmddyyyy-hhmmss