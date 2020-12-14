---
title: sql transaction
author: PipisCrew
date: 2015-12-09
categories: [sql]
toc: true
---

STEP 1 :
```js
	use mydbase

	begin tran

	select * from Product where Product_ID = 22236

	UPDATE product 
	SET    price1 = '685', 
		   price2 = '556.91' 
	WHERE  product_id = 22236 

	select * from Product where Product_ID = 22236
``` 

STEP 2 :
```js 
 #if we like what we see run commit otherwise rollback#
	--rollback
	--commit
``` 

#rollback #commit #tran

origin - http://www.pipiscrew.com/?p=2762 sql-sql-transaction