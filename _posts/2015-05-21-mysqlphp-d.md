---
title: o[mysql+php] date conversions
author: PipisCrew
date: 2015-05-21
categories: []
toc: true
---

**MySQL Query - Subtract CURDATE on DATE fieldtype**
ex. when 30/12
where record date is equal today 30/12 OR record date == 23/12
```js
SELECT DATE_FORMAT(next_renewal,'%d/%m/%Y') as test FROM offers
WHERE marketing_plan_completed=1 and
(next_renewal = CURDATE() or next_renewal = DATE_SUB(CURDATE(), INTERVAL 7 DAY))
```

^this one, can modified to result every day, till pass the record date, using BETWEEN, in detail :
```js
SELECT DATE_FORMAT(next_renewal,'%d/%m/%Y') as test FROM offers
WHERE marketing_plan_completed=1 and
(next_renewal BETWEEN DATE_SUB(CURDATE(), INTERVAL 30 DAY) AND CURDATE())
```

**MySQL Query - Between CURDATE on DATETIME fieldtype**
```js
select DATE_FORMAT(marketing_plan_when,'%d-%m-%Y %H:%i') as test from offers 
WHERE marketing_plan_completed=0 and 
marketing_plan_when between CONCAT(CURDATE() , ' ', '00:00')
 and CONCAT(CURDATE() , ' ', '23:59')
```

**MySQL Query - DATETIME field only for TIME part**
```js
--this result records 10:00 - 10:05 including 10:05
SELECT *
FROM  user_working_hours
WHERE EXTRACT(HOUR_SECOND from date_start) between 100000 and 100500

--result when date_start 10:00:00-10:05:60 and 15:30:00-15:31:00
SELECT *
FROM  user_working_hours
WHERE (EXTRACT(HOUR_SECOND from date_start) between 100000 and 100600)
AND (EXTRACT(HOUR_SECOND from date_end) between 153000 and 153100)
```

**PHP Now Formatted with leading zeros**
```jsdate("Y-m-d H:i:s")```

**PHP - Cast to valid MySQL date**
```js
if (!isset($_POST['client_appointment_datetime']))
         die("Error");

$client_appointment_datetime=null;
if (!empty($_POST['client_appointment_datetime']))
{
   $dt = DateTime::createFromFormat('d-m-Y H:i', $_POST['client_appointment_datetime']);

   $client_appointment_datetime = $dt->format('Y-m-d H:i:s'); //valid for MySQL
}
```

**FYI MySQL**

> now() = 2014-12-03 08:51:15
> CURDATE()) = 2014-12-03
> CURTIME() = 08:51:15

* * *

### The start of the current month

```js
select DATE_FORMAT(NOW() ,'%Y-%m-01');
```

### The end of the current month

```js
SELECT LAST_DAY(CURDATE()); 
```

### Add months to date

```js
//http://www.w3schools.com/sql/func_date_add.asp
SELECT DATE_ADD(CURDATE(),INTERVAL 3 MONTH) , CURDATE();  
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap047.png "snap047")

* * *

```js
//table fields on where :
//offer_contract_period
//is_paid_when
//yeah we can use db field on where, in date_add function what a cute thing!!! + subtract!!!

select offer_id, offer_company_name,offer_contract_period,is_paid_when,DATE_ADD(is_paid_when,INTERVAL (offer_contract_period-1) MONTH) from offers
WHERE 
(DATE_FORMAT(NOW() ,'%Y-%m-01') between is_paid_when and DATE_ADD(is_paid_when,INTERVAL (offer_contract_period-1) MONTH))
OR
(LAST_DAY('2015-05-21') between is_paid_when and DATE_ADD(is_paid_when,INTERVAL (offer_contract_period-1) MONTH))
```

origin - http://www.pipiscrew.com/?p=2070 mysqlphp-date-conversions