---
title: YaLinqo (LINQ)
author: PipisCrew
date: 2017-02-08
categories: [php]
toc: true
---

Tried once and stuck with **YaLinqo**, check this : 

YaLinqo - Github - https://github.com/Athari/YaLinqo
YaLinqo - doc - https://athari.github.io/YaLinqo/

```js
CREATE TABLE `user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `email` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `firstname` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `lastname` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `age` int(11) DEFAULT NULL,
  `country` char(2) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email` (`email`)
) ENGINE=InnoDB AUTO_INCREMENT=51 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;```

Author suggests to use composer w/ autoloaded.php, Im too lazy go that way, when the lib is only **8** files.

```js
//my tests
<?php require_once('/yalinqo/utils.php');="" require_once('/yalinqo/functions.php');="" require_once('/yalinqo/linq.php');="" require_once('/yalinqo/enumerablepagination.php');="" require_once('/yalinqo/enumerablegeneration.php');="" require_once('/yalinqo/enumerable.php');="" require_once('/yalinqo/errors.php');="" require_once('/yalinqo/orderedenumerable.php');="" require_once('general.php');="" connect="" via="" pdo="" $db="connect_mysql();" select="" a="" table="" $rows="getSet($db," select"="" *="" from="" user",null);="" returns="" all="" records="" sorted="" by="" column="" #country#="" $result3="from($rows)" -=""?>orderBy(function ($cat) { return $cat['country']; });

echo "

";
    var_dump($result3->toArray());
    echo "
";

//this equals with 

$result3 = from($rows)
->orderBy(function ($cat) { return $cat['country']; })
->toArray();

echo "

";
    var_dump($result3);
    echo "
";

--

//returns all array records sorted DESC by column #country#
$result3 = from($rows)
->orderByDescending(function ($cat) { return $cat['country']; })
->toArray();

echo "

";
    var_dump($result3);
    echo "
";

//returns all the records where the field #country# equals 'au',
//(as you see Im using strtolower, because is case sensitive)
//then order by #email# field and return only the columns
//country,email. If you remove the ->select line will return all fields
$result3 = from($rows)
->where(function ($x) { return strtolower($x['country'])=='au'; })
->orderBy(function ($y) { return $y['email']; })
->select(function($res){ return array(
                "country" => $res['country'],
                "age" => $res['email']
            ); })
->toArray();

echo "

";
    var_dump($result3);
    echo "
";

--

//groupby country - method1
$result3 = from($rows)
->groupBy(function ($y) { return $y['country']; })
->toArray();

echo "

";
    var_dump($result3);
    echo "
";

//this equals with 

$result3 = from($rows)
->groupBy('$v["country"]')
->toArray();

echo "

";
    var_dump($result3);
    echo "
";
```

**Athari** said :

> Grouping by multiple keys produces a bit too nested code, so you can write helper methods like this:

```js
//https://github.com/Athari/YaLinqo/issues/19#issuecomment-209270090
function group_by_multiple ($items, array $keySelectors, $valueSelector = null)
{
    $resultSelector = null;
    foreach (array_reverse($keySelectors) as $keySelector) {
        $resultSelector = function ($subitems) use ($keySelector, $valueSelector, $resultSelector) {
            return from($subitems)->groupBy(
                $keySelector,
                $resultSelector == null ? $valueSelector : null,
                $resultSelector);
        };
    }
    return $resultSelector($items);
}

print_r(
    group_by_multiple($items,
        [ '$v["category"]', '$v["group"]', '$v["name"]' ],
        '$v["name"]'
    )->toArrayDeep());
```

And the time come, to use it for date queries.

My first attempt :
```js
//the $rows is a PDO recordset (aka plain array), to make it work
//I have to #cast# the array element came from MySQL datetime field #datecreated#
//to date, so PHP understand the comparison, right ?
$result3 = from($rows)
->where(function ($x) { return 
DateTime::createFromFormat("Y-m-d H:i:s", $x['datecreated']) >= DateTime::createFromFormat("Y-m-d H:i:s","2017-02-12 00:00:00") && 
DateTime::createFromFormat("Y-m-d H:i:s", $x['datecreated']) < datetime::createfromformat("y-m-d="" h:i:s","2017-02-15="" 00:00:00");="" })="" -="">select(function($res){ return array(
            "country" => $res['country'],
            "datecreated" => $res['datecreated']
        ); })
->toArray();

echo "

";
    var_dump($result3);
    echo "
";
```

ok, works, but nah... too much trouble in the world.. this also can work, when no time specified assume 00:00:00

```js
//use of #strtotime# (aka parse to Unix timestamp)
$result3 = from($rows)
->where(function ($x) { return 
strtotime($x['datecreated']) >= strtotime("2017-02-12") && 
strtotime($x['datecreated']) < strtotime("2017-02-15");="" })="" -="">select(function($res){ return array(
            "country" => $res['country'],
            "datecreated" => $res['datecreated']
        ); })
->toArray();
```

one more option is to cast it to **DateTime** , but the best solution indeed is the **strtotime**.
```js
function str2date($src_val, $date_format = "Y-m-d H:i:s"){
    if ($src_val==null || startsWith($src_val, "0000")) //the date is null (aka SQL - date NULL) OR is empty (aka year is 0000)
       return null;

    //[start] validation if the $src_val contains space
    $src_val = trim($src_val);

    if (strpos($src_val, ' ')==0){
        //occur when the date_format doesnt contain H:i:s - PHP automatically adds the current time!!
        $src_val .= " 00:00:00";
    }
    //[end] validation if the $src_val contains space

    $d = DateTime::createFromFormat($date_format, $src_val);

    if (!$d)
       throw new Exception("string cant be converted to date >> ".$src_val);
    else
        return $d;
}

$result3 = from($rows)
->where(function ($x) { return 
str2date($x['datecreated']) >= str2date("2017-02-12") && 
str2date($x['datecreated']) < str2date("2017-02-15");="" })="" -="">select(function($res){ return array(
            "country" => $res['country'],
            "datecreated" => $res['datecreated']
        ); })
->toArray();
```

> Using DateTime::createFromFormat - PHP automatically adds the current time!!

image the dbase #datacreated# column :
2017-02-12
2017-02-13
2017-02-14
2017-02-15

if you dont use the fix for time (line 9), and query via ##<strong style='color:red'>>=** str2date("2017-02-12")##
the 2017-02-12 record will not come!!!!

But why to use LINQ? 
-you can sort/order/select anything in one line!

* * *

Lets see what **mcaskill**, hang at gists :
```js
//src - https://gist.github.com/mcaskill/baaee44487653e1afc0d
//test.php
require_once 'Function.Array-Group-By.php';

//based on above example $rows contains PDO recordset
$result3 = array_group_by($rows, "country","age" );

//here the recordset i grouped by 2 levels
-Country
--age
echo "

";
    var_dump($result3);
    echo "
";

//Function.Array-Group-By.php
<?php if="" (="" !="" function_exists('array_group_by')="" )="" :="" **="" *="" groups="" an="" array="" by="" a="" given="" key.="" *="" *="" groups="" an="" array="" into="" arrays="" by="" a="" given="" key,="" or="" set="" of="" keys,="" shared="" between="" all="" array="" members.="" *="" *="" based="" on="" {@author="" jake="" zatecky}'s="" {@link="" https://github.com/jakezatecky/array_group_by="" array_group_by()}="" function.="" *="" this="" variant="" allows="" $key="" to="" be="" closures.="" *="" *="" @param="" array="" $array="" the="" array="" to="" have="" grouping="" performed="" on.="" *="" @param="" mixed="" $key,...="" the="" key="" to="" group="" or="" split="" by.="" can="" be="" a="" _string_,="" *="" an="" _integer_,="" a="" _float_,="" or="" a="" _callable_.="" *="" *="" if="" the="" key="" is="" a="" callback,="" it="" must="" return="" *="" a="" valid="" key="" from="" the="" array.="" *="" *="" ```="" *="" string|int="" callback="" (="" mixed="" $item="" )="" *="" ```="" *="" *="" @return="" array|null="" returns="" a="" multidimensional="" array="" or="" `null`="" if="" `$key`="" is="" invalid.="" */="" function="" array_group_by(="" array="" $array,="" $key="" )="" {="" if="" (="" !="" is_string(="" $key="" )="" &&="" !="" is_int(="" $key="" )="" &&="" !="" is_float(="" $key="" )="" &&="" !="" is_callable(="" $key="" )="" )="" {="" trigger_error(="" 'array_group_by():="" the="" key="" should="" be="" a="" string,="" an="" integer,="" or="" a="" callback',="" e_user_error="" );="" return="" null;="" }="" $func="(" is_callable(="" $key="" )="" $key="" :="" null="" );="" $_key="$key;" load="" the="" new="" array,="" splitting="" by="" the="" target="" key="" $grouped="[];" foreach="" (="" $array="" as="" $value="" )="" {="" if="" (="" is_callable(="" $func="" )="" )="" {="" $key="call_user_func(" $func,="" $value="" );="" }="" elseif="" (="" is_object(="" $value="" )="" &&="" isset(="" $value-=""?>{ $_key } ) ) {
				$key = $value->{ $_key };
			} elseif ( isset( $value[ $_key ] ) ) {
				$key = $value[ $_key ];
			} else {
				continue;
			}
			$grouped[ $key ][] = $value;
		}
		// Recursively build a nested grouping if more parameters are supplied
		// Each grouped array value is grouped according to the next sequential key
		if ( func_num_args() > 2 ) {
			$args = func_get_args();
			foreach ( $grouped as $key => $value ) {
				$params = array_merge( [ $value ], array_slice( $args, 2, func_num_args() ) );
				$grouped[ $key ] = call_user_func_array( 'array_group_by', $params );
			}
		}
		return $grouped;
	}
endif;
```

the result :
```js
  ["Sa"]=>
  array(3) {
    [4]=>
    array(2) {
      [0]=>
      array(6) {
        ["id"]=>
        string(1) "6"
        ["email"]=>
        string(29) "jessica.gutkowski@example.net"
        ["firstname"]=>
        string(8) "Cordelia"
        ["lastname"]=>
        string(9) "Romaguera"
        ["age"]=>
        string(1) "4"
        ["country"]=>
        string(2) "Sa"
      }
      [1]=>
      array(6) {
        ["id"]=>
        string(2) "27"
        ["email"]=>
        string(25) "hartmann.bart@example.org"
        ["firstname"]=>
        string(5) "Lonie"
        ["lastname"]=>
        string(10) "Stiedemann"
        ["age"]=>
        string(1) "4"
        ["country"]=>
        string(2) "Sa"
      }
    }
    [6]=>
    array(2) {
      [0]=>
      array(6) {
        ["id"]=>
        string(2) "11"
        ["email"]=>
        string(19) "pbednar@example.com"
        ["firstname"]=>
        string(5) "Sonny"
        ["lastname"]=>
        string(8) "Nikolaus"
        ["age"]=>
        string(1) "6"
        ["country"]=>
        string(2) "Sa"
      }
      [1]=>
      array(6) {
        ["id"]=>
        string(2) "20"
        ["email"]=>
        string(23) "leannon.roy@example.com"
        ["firstname"]=>
        string(4) "Olaf"
        ["lastname"]=>
        string(7) "Kuvalis"
        ["age"]=>
        string(1) "6"
        ["country"]=>
        string(2) "Sa"
      }
    }
    [3]=>
    array(1) {
      [0]=>
      array(6) {
        ["id"]=>
        string(2) "26"
        ["email"]=>
        string(24) "vesta.gibson@example.net"
        ["firstname"]=>
        string(6) "Juliet"
        ["lastname"]=>
        string(9) "Buckridge"
        ["age"]=>
        string(1) "3"
        ["country"]=>
        string(2) "Sa"
      }
    }
  }
```

### LINQ for PHP comparison: YaLinqo, Ginq, Pinq

https://www.codeproject.com/articles/997238/linq-for-php-comparison-yalinqo-ginq-pinq</strong>

origin - http://www.pipiscrew.com/?p=6644 php-yalinqo-linq