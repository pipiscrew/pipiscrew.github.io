---
title: export dbase to csv with criteria
author: PipisCrew
date: 2015-08-31
categories: [Uncategorized]
toc: true
---

reference 
[http://www.the-art-of-web.com/dataexport1.phps](http://www.the-art-of-web.com/dataexport1.phps)

```js
//index.html
<form method="POST" action="export.php">
				<div class='form-group'>
					<label>Country :</label>
					<select name="country" class='form-control'></select>
				</div>

				<div class='form-group'>
					<label>Loyalty :</label>
					<select name="loyalty" class='form-control'></select>
				</div>

				<div class='form-group'>
					<label>Pump Type :</label>
					<select name="pump_type" class='form-control'></select>
				</div>

				<button class="btn btn-primary" type="submit">Export</button>
</form>
```

```js
//export.php
<?php require_once("config.php");="" if="" (!isset($_post["country"])="" ||="" !isset($_post["loyalty"])="" ||="" !isset($_post["pump_type"])){="" die("error="" 6x9568");="" }="" $db="connect();" $country="$_POST["country"];" $loyalty="$_POST["loyalty"];" $pump_type="$_POST["pump_type"];" $wh="" ;="" if="" ($country=""?>0)
	$wh = "where members.country_id={$country}"; 

if ($pump_type>0)
{
	if (strlen($wh)>0)
		$wh.= " and ";
	else 
		$wh.= " where ";

	$wh .= " members.pump_type_id={$pump_type} "; 
}

if (strlen($loyalty)>0)
{
	if (strlen($wh)>0)
		$wh.= " and ";
	else 
		$wh.= " where ";

	$wh .= " loyalty like '%{$loyalty}%' "; 
}	

if ($stmt = $db -> prepare("select member_id,concat(first_name, ' ', last_name , ' ', middle_name) as fullname,email,pump_type_name, country_name, phone1, phone2, special_title, loyalty, special_field_interest, website, facebook, twitter, date_created, date_approved
from members 
left join pump_types on pump_types.pump_type_id = members.pump_type_id 
left join countries on countries.country_id = members.country_id {$wh} order by fullname")) {

		$stmt->execute($params);

		$db_set = $stmt->fetchAll(PDO::FETCH_ASSOC);
}

//Original PHP code by Chirp Internet: www.chirp.com.au
function cleanData(&$str)
{
	$str = preg_replace("/\t/", "\\t", $str);
	$str = preg_replace("/\r?\n/", "\\n", $str);
	if(strstr($str, '"')) $str = '"' . str_replace('"', '""', $str) . '"';
}

// file name for download
$filename = "website_data_" . date('Ymd') . ".xls";

header("Content-Disposition: attachment; filename=\"$filename\"");
header("Content-Type: application/vnd.ms-excel");

$flag = false;
foreach($db_set as $row) {
	if(!$flag) {
	  // display field/column names as first row
	  echo implode("\t", array_keys($row)) . "\n";
	  $flag = true;
	}
	array_walk($row, 'cleanData');
	echo implode("\t", array_values($row)) . "\n";
}
```

origin - http://www.pipiscrew.com/?p=1770 php-export-dbase-to-csv-with-criteria