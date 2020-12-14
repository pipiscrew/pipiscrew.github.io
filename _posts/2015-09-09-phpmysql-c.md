---
title: o[php+mysql] comments system
author: PipisCrew
date: 2015-09-09
categories: [css,sql]
toc: true
---

reference
[http://www.9lessons.info/2009/09/comment-system-database-with-jquery.html](http://www.9lessons.info/2009/09/comment-system-database-with-jquery.html)

```js
<style>
	.commentauthor {
	  color: #333333;
	  font-size: 14px;
	  font-weight: bold;
	  text-decoration: none;
	}
	.commentfooter {
	  margin-bottom: 10px;
	  border: dashed 2px #48B1D9;
	  border-top: none;
	}
	.commenttimestamp {
	  font-size: 11px;
	  padding-left: 10px;
	  color: #666666;
	}
	.commentbody {
	  font-size: 15px;
	  color: #3A4145;
	  border: dashed 2px #48B1D9;
	  padding: 10px;
	  border-bottom: none;
	  word-wrap: break-word;
	}
	.txt_submit {
	  color: #000000;
	  font-size: 14px;
	  border: #666666 solid 2px;
	  height: 124px;
	  margin-bottom: 10px;
	  width: 200px;
	}
	.txt_multi {
	  color: #000000;
	  font-size: 14px;
	  border: #666666 solid 2px;
	  height: 124px;
	  margin-bottom: 10px;
	  width: 400px;
	}
</style>

	<div class="container">
<?php $db_comments="getSet($db,"select" *,="" concat(first_name,'="" ',last_name,'="" ',last_name)="" as="" author_name,date_format(daterec,'%d="" %b,="" %y="" %k:%i')="" as="" daterec2="" from="" new_comment="" left="" join="" members="" on="" members.member_id="new_comment.member_id" where="" new_id="?" order="" by="" daterec="" desc",array($news_id));="" $template="<div class='commentauthor'>#author#</div><p class='commentbody'>#comment#</p><div class='commentfooter'><span class='commenttimestamp'>#timestamp#</span></div>" ;="" foreach($db_comments="" as="" $row)="" {="" $searchreplacearray="array(" '#author#'=""?> $row['author_name'], 
								  '#comment#' => $row['comment'],
								  '#timestamp#' => $row['daterec2']
								);
		echo  str_replace(
						  array_keys($searchReplaceArray), 
						  array_values($searchReplaceArray), 
						  $template
						);
	}
?>

<?php if="" (isset($_session["member_id"]))="" {=""?>
		<form action="new_add.php" method="post">
		<textarea name="comment" style="resize:none;" class="txt_multi" id="comment"></textarea>
		<input name="new_id" style="visibility: hidden;" value="<?=$_GET['id'];?>">  

		<button type="submit" name="submit">submit</button>
		</form>
<?php }=""?>

	</div>
```

```js
//new_add.php
<?php @session_start();="" include('config.php');="" $db="connect();" when="" submit="" comment="" if="" ($_server['request_method']="==" 'post'="" &&="" isset($_post["comment"])="" &&="" isset($_post["new_id"]))="" {="" $sql="INSERT INTO `new_comment` (new_id, member_id, comment, daterec) VALUES (:new_id, :member_id, :comment, :daterec)" ;="" $stmt="$db-"?>prepare($sql);

	$stmt->bindValue(':new_id' , $_POST['new_id']);
	$stmt->bindValue(':member_id' , $_SESSION["member_id"]);
	$stmt->bindValue(':comment' , $_POST['comment']);
	$stmt->bindValue(':daterec' , date("Y-m-d H:i:s"));

	$stmt->execute();	

	header("Location:news_detail.php?id={$_POST['new_id']}");
} 
?>
```

```js
CREATE TABLE `news` (
  `news_id` int(11) NOT NULL AUTO_INCREMENT,
  `member_id` int(11) DEFAULT NULL,
  `news_tile` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
  `news_descr` text COLLATE utf8_unicode_ci,
  `news_is_active` tinyint(3) NOT NULL DEFAULT '0',
  `news_order_id` int(11) NOT NULL DEFAULT '0',
  `news_daterec` datetime DEFAULT NULL,
  `news_is_free` tinyint(3) NOT NULL DEFAULT '0',
  PRIMARY KEY (`news_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```

origin - http://www.pipiscrew.com/?p=1895 phpmysql-comments-system