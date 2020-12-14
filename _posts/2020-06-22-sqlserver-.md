---
title: SQLServer - Working with XML field
author: PipisCrew
date: 2020-06-22
categories: [sql]
toc: true
---

On a table field, example :

```js
select field from table
```

the field type is XML, a sample record :
```js
--sample xml
<?xml version="1.0" encoding="UTF-8"?>
<item id="9055">
   <resource>
      <size>
         <imagetype id="1" code="Large"></imagetype>
         <imagetype id="2" code="Normal"></imagetype>
      </size>
      <meta>
         <lang id="1" code="el"></lang>
         <lang id="9" code="el"></lang>

   </resource>
</item>
```

* * *

## Group By

select the Meta.code only
```js
--src https://stackoverflow.com/a/19165348
SELECT 
X.Y.value('@code', 'varchar(3)')
FROM table imr 
OUTER APPLY imr.field.nodes('Item/Resource/Meta/lang') as X(Y)
```

group by Meta.code to get the unique values of the xml attribute

if you do 
```js
SELECT 
X.Y.value('@code', 'varchar(3)') AS lng
FROM table imr 
OUTER APPLY imr.field.nodes('Item/Resource/Meta/lang') as X(Y)
GROUP BY X.Y.value('@code', 'varchar(3)')
```

will get

> Msg 4148, XML methods are not allowed in a GROUP BY clause.

use it as subquery then group by the field
```js
--src https://stackoverflow.com/a/22662302
SELECT lng
	FROM (
		SELECT 
		X.Y.value('@code', 'varchar(3)') AS lng
		FROM table imr 
		OUTER APPLY imr.field.nodes('Item/Resource/Meta/lang') as X(Y)
	) AS t
GROUP BY lng
```

* * *

## Query all records have attribute equal to

this will scan all **lang** sub nodes of **Meta** element for the given attribute (aka id)
```js
--src https://www.sqlshack.com/filtering-xml-columns-using-xquery-in-sql-server/
SELECT  
COUNT(*)
FROM table
WHERE field.exist('(Item/Resource/Meta/lang/@id[.="9"])') = 1
```

the below, scans for each record, the second element **Meta/lang** for the given attribute (aka id)
```js
SELECT 
COUNT(*)
FROM table
WHERE field.value('(Item/Resource/Meta/lang/@id)[2]', 'varchar(3)') <> '9'
```

* * *

## Insert extra element with attributes to existing XML record

```js
--src https://www.mssqltips.com/sqlservertip/2738/examples-of-using-xquery-to-update-xml-data-in-sql-server/
-- https://www.sqlshack.com/different-ways-to-update-xml-using-xquery-in-sql-server/
UPDATE table
SET field.modify('insert <lang id="9" code="ro"></lang> into (Item/Resource/Meta)[1]')
WHERE id=8
```

origin - https://www.pipiscrew.com/?p=18545 sqlserver-working-with-xml-field