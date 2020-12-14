---
title: Rebuild FullText
author: PipisCrew
date: 2016-02-25
categories: [sql]
toc: true
---

Find the Name

```js
select * from sys.fulltext_catalogs
```

Rebuilt via : 
ALTER FULLTEXT CATALOG #name# rebuild

origin - http://www.pipiscrew.com/?p=4001 sql-rebuild-fulltext