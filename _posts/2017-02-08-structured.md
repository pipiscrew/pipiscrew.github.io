---
title: structured array
author: PipisCrew
date: 2017-02-08
categories: [php]
toc: true
---

```js
//test.php
class poster_rec {
	public $offer_id;

	public $user_id;
	public $user_name;

	public $company_id;
	public $company_name;

	public $ad_type;

	public $ad_price_daily_default;
	public $ad_price_user;
	public $ad_conversion;
}

//will be [list of poster_rec]
$ListOfPosterRECS=null;

//poster_rec itself
$rec_poster=null;
.
.
$users = getSet($db,"select * from users",null);
.
.

//for each row
foreach($users as $user_row) {

	$rec_poster = new poster_rec();
	$rec_poster->offer_id = $user_row["offer_id"];
	$rec_poster->user_id = $user_row["user_id"];
	$rec_poster->user_name = $user_row["fullname"];
	$rec_poster->company_id = $user_row["company_id"];
	$rec_poster->company_name = $user_row["offer_company_name"];
	$rec_poster->ad_type = $user_row["obj_type"];
	.
	.
	.
	//add to [list of poster_rec]
	$ListOfPosterRECS[] = $rec_poster;
}

//output
echo '

' . print_r($ListOfPosterRECS,1) . '
';

//loop through
for ($x=0; $x <= sizeof($listofposterrecs);="" $x++){="" echo="" $listofposterrecs[$x]-="">offer_id."  
";
}
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/03/snap597.png "snap597")

* * *

Matt (http://www.webmaster-source.com/2009/08/20/php-stdclass-storing-data-object-instead-array/) writes : 

> Using PHP’s stdClass feature you can create an object, and assign data to it, without having to formally define a class. Suppose you wanted to quickly create a new object to hold some data about a book. You would do something like this:

```js
//test2.php
$book = new stdClass;
$book->title = "Harry Potter and the Prisoner of Azkaban";
$book->author = "J. K. Rowling";
$book->publisher = "Arthur A. Levine Books";
$book->amazon_link = "http://www.amazon.com/dp/0439136369/";

echo '

' . print_r($book,1) . '
';
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/03/snap598.png "snap598")

or as :
```js
class MyClass {
  public $ID;
}

$object = new MyClass();
$object->ID = 'foo';
echo $object->ID;
```

> Or what if you wanted to take an array and turn it into an object? You can do that by casting the variable.

```js
//test3.php
$array = array(
"title" => "Harry Potter and the Prisoner of Azkaban",
"author" => "J. K. Rowling",
"publisher" => "Arthur A. Levine Books",
"amazon_link" => "http://www.amazon.com/dp/0439136369/"
);

$books = (object) $array;

echo '

' . print_r($books,1) . '
';
?>
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/03/snap599.png "snap599")

### Collection Classes in PHP

https://www.sitepoint.com/collection-classes-in-php/</=>

origin - http://www.pipiscrew.com/?p=2762 php-structured-array