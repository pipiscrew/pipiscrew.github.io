---
title: o[php+mysql] get working days between dates
author: PipisCrew
date: 2014-10-20
categories: []
toc: true
---

the table
```js
CREATE TABLE user_vacations (
  user_vacation_id int(11) NOT NULL AUTO_INCREMENT,
  user_id int(11) DEFAULT NULL,
  date_start date DEFAULT NULL,
  date_end date DEFAULT NULL,
  authorized tinyint(4) DEFAULT NULL,
  comment varchar(200) COLLATE utf8_unicode_ci DEFAULT NULL,
  PRIMARY KEY (user_vacation_id)
) ENGINE=MyISAM AUTO_INCREMENT=11 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

-- ----------------------------
-- Records of user_vacations
-- ----------------------------
INSERT INTO user_vacations VALUES ('1', '3', '2014-10-25', '2014-10-26', '0', '123');
INSERT INTO user_vacations VALUES ('2', '3', '2014-10-16', '2014-10-17', '1', '123');
INSERT INTO user_vacations VALUES ('8', '3', '2014-10-31', '2014-11-09', '0', 'x');
INSERT INTO user_vacations VALUES ('9', '3', '2014-10-20', '2014-10-21', '1', 'x23');
INSERT INTO user_vacations VALUES ('7', '1', '2014-10-17', '2014-10-17', '0', '879');
INSERT INTO user_vacations VALUES ('10', '1', '2014-10-31', '2014-11-11', '1', 'sadfs');
```

the code
```js
$sql = "select DATE_FORMAT(date_start,'%Y-%m-%d') as date_start,DATE_FORMAT(date_end,'%Y-%m-%d') as date_end interval from user_vacations where date_start is not null and date_end is not null";

foreach($rows as $row) {
	echo $row['date_start'] . ", ".$row['date_end'].'#'.getWorkingDays($row['date_start'],$row['date_end'])."  
";
}

//cut-down version of 
//http://mugurel.sumanariu.ro/php-2/php-how-to-calculate-number-of-work-days-between-2-dates/
function getWorkingDays($startDate, $endDate)	{
	$begin   = strtotime($startDate);
	$end     = strtotime($endDate);

	$no_days = 0;

	while($begin < $end)="" {="" $what_day="date("N",$begin);" if($what_day="">< 6)="" 6="" and="" 7="" are="" weekend="" days="" $no_days++;="" $begin="" +="86400;" +1="" day="" };="" return="" $no_days;="" }="" ```="" the="" result="">![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap092.png "snap092")

where with natural SQL query :
```js
SELECT DATE_FORMAT(date_start,'%Y-%m-%d') as date_start,DATE_FORMAT(date_end,'%Y-%m-%d') as date_end,datediff(date_end,date_start) as diff FROM user_vacations 
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap093.png "snap093")

origin - http://www.pipiscrew.com/?p=1569 phpmysql-get-working-days-between-dates