---
title: search and replace
author: PipisCrew
date: 2016-03-04
categories: [sql]
toc: true
---

```js
--http://stackoverflow.com/a/4350529
update CMS_News set img_fullpath=REPLACE(img_fullpath, 'amazon/pipiscrew', 'pipiscrew'),
large_img=REPLACE(large_img, 'amazon/pipiscrew', 'pipiscrew')
where CategoryID = 18

select REPLACE(img_fullpath, 'amazon/pipiscrew', 'pipiscrew'),REPLACE(large_img, 'amazon/pipiscrew', 'pipiscrew') from CMS_News
where CategoryID = 18
```

#SnR

origin - http://www.pipiscrew.com/?p=4201 sql-search-and-replace