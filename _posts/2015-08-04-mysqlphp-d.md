---
title: o[mysql+php] dateformat function - creating a timetable
author: PipisCrew
date: 2015-08-04
categories: []
toc: true
---

reference 
[http://www.w3schools.com/sql/func_date_format.asp](http://www.w3schools.com/sql/func_date_format.asp)

![](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap247.png "snap247")

using the mysql date_format will help me to split the date by the time and vice versa..

```js
//test
<div style="font-family: 'Roboto', sans-serif;font-size:26px;font-weight: bold;color:#B0166C;"> Program</div>
<?php $timetable="getSet($db," select"="" event_timeline_id,date_format(event_timeline_time,'%d="" %b,="" %y')="" as="" eventdate,="" date_format(event_timeline_time,'%h:%i')="" as="" eventtime,event_timeline_descr="" from="" event_timeline="" where="" event_id="?" order="" by="" event_timeline_time="" asc",array($event_id));="" $last_datetime="" ;="" $day="0;" foreach="" ($timetable="" as="" $time)="" {="" if="" ($last_datetime!="$time['eventdate'])" {="" echo=""?><div style='margin-bottom:5px;border-bottom:3px #B0166C solid'> </div>";
 				$day+=1;

				echo "<span style="\" font-family:"="" 'roboto',="" sans-serif;font-size:23px;font-weight:="" bold;color:#b0166c;\"=""> Day {$day} : </span><span style="\" font-family:"="" 'roboto',="" sans-serif;font-size:23px;font-weight:="" bold;color:#000000;\"="">{$time['eventdate']}</span>  

";
			}
			else 
				echo "

* * *
";

			echo "<span style="\" font-family:"="" 'roboto',="" sans-serif;font-size:18px;font-weight:="" bold;color:#b0166c;\"=""> {$time['eventtime']} </span><span style="\" font-family:"="" 'roboto',="" sans-serif;font-size:18px;color:#000000;\"="">{$time['event_timeline_descr']}</span>";

 			$last_datetime = $time['eventdate'];
 		}
?>
```

the dbase records
![](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap249.png "snap249")

running my query 
```js
select event_timeline_id,DATE_FORMAT(event_timeline_time,'%d %b, %Y') as eventdate, DATE_FORMAT(event_timeline_time,'%H:%i') as eventtime,event_timeline_descr from event_timeline where event_id=? order by event_timeline_time ASC
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap251.png "snap251")

the result :
![](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap250.png "snap250")

```js
CREATE TABLE event_timeline (
  event_timeline_id int(11) NOT NULL AUTO_INCREMENT,
  event_id int(11) DEFAULT NULL,
  event_timeline_time datetime DEFAULT NULL,
  event_timeline_descr text COLLATE utf8_unicode_ci,
  PRIMARY KEY (event_timeline_id)
) ENGINE=InnoDB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```

origin - http://www.pipiscrew.com/?p=3563 mysql-dateformat-function-creating-a-timetable