---
title: o[mysql] query datetime field only by time
author: PipisCrew
date: 2014-10-30
categories: []
toc: true
---

we have these records :
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap133.png "snap133")

using :
```js
SELECT *
FROM  user_working_hours
WHERE EXTRACT(HOUR_SECOND from date_start) between 100000 and 100500
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap134.png "snap134")

using :
```js
SELECT *
FROM  user_working_hours
WHERE EXTRACT(HOUR_SECOND from date_start) between 100000 and 100600
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap135.png "snap135")

using :
```js
SELECT *
FROM  user_working_hours
WHERE (EXTRACT(HOUR_SECOND from date_start) between 100000 and 100600) AND (EXTRACT(HOUR_SECOND from date_end) between 153000 and 153100)
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap136.png "snap136")

just for the history, using :
```js
SELECT *
FROM  user_working_hours
WHERE HOUR(date_start)>15
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap137.png "snap137")

origin - http://www.pipiscrew.com/?p=1658 mysql-query-datetime-field-only-by-time