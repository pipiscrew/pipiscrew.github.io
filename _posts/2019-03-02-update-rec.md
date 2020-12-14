---
title: update records via join table
author: PipisCrew
date: 2019-03-02
categories: [sql]
toc: true
---

# way 1

```js
UPDATE Products
SET Product_Code = Toys.codename
FROM Products
INNER JOIN Toys ON Toys._ID = Products.Toy_ID
WHERE Products.Language_ID = 1;
```

# way 2

```js
with tmp_tbl as (
	select Product_ID from PRODUCTies
	group by Product_ID
)
Update PRODUCTS
	Set Product_Price = 0
Where Product_ID in (Select Product_ID From tmp_tbl Where xyz = 0 )
```

# way 3

```js
update products set 
payable  = 1,
price = isnull(t.price, products.price) ,
pieces = t.total_pieces
from
(
	select m.id, lz.* 
	from tableC lz
	inner join products tableB on tableB.fieldA = lz.fieldA collate Greek_CI_AS and tableB.fieldB = lz.fieldB collate Greek_CI_AS
) t
where t.id = products.id
```

origin - http://www.pipiscrew.com/?p=2903 sql-update-records-via-join-table