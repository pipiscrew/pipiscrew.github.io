---
title: o[mysql] mysql backup
author: PipisCrew
date: 2015-07-21
categories: []
toc: true
---

reference
[http://davidwalsh.name/backup-mysql-database-php](http://davidwalsh.name/backup-mysql-database-php)

[http://mihaifrentiu.com/mysql-backup-php-helper](http://mihaifrentiu.com/mysql-backup-php-helper)

writes :
If you want to skip entering the credentials every time, just fill these variables in the php code of the file:
```js
$db_host = '';
$db_name = '';
$db_user = '';
$db_pass = '';
```
and the form fields will be auto completed.

<strong style="color:red">VERY IMPORTANT: MAKE SURE YOU UPLOAD THE FILE IN A SECURE FOLDER,  NOT PUBLIC. I STRONGLY RECOMMEND YOU UPLOAD IT TO A .HTACCESS PASSWORDED FOLDER.**
  [http://davidwalsh.name/password-protect-directory-using-htaccess](http://davidwalsh.name/password-protect-directory-using-htaccess)
htpasswd - The password will be stored in encrypted form (standard crypt function) and the username will be in plaintext. more at [http://stackoverflow.com/a/4175789](http://stackoverflow.com/a/4175789) - generate a password at [http://davidwalsh.name/web-development-tools](http://davidwalsh.name/web-development-tools)

lines added  -  UTF8 (line 56) and exit (line 116)

```js
//author : http://mihaifrentiu.com/mysql-backup-php-helper
//filename : mf_mysql_backup.php
<?php *="" author:="" mihai="" frentiu="" author="" url:="" http://mihaifrentiu.com="" license:="" gpl="" v2="" or="" higher="" based="" on:="" http://davidwalsh.name/backup-mysql-database-php="" */="" $db_host='' ;="" $db_name='' ;="" $db_user='' ;="" $db_pass='' ;="" $err="false;" $connected="false;" if(isset($_post)="" &&="" isset($_post['submit'])){="" check="" if="" the="" db="" host="" came="" on="" post="" if(isset($_post['db_host'])="" &&="" $_post['db_host']="" !='' ){="" $db_host="$_POST['db_host'];" }else{="" $err="true;" $err_host="true;" }="" check="" if="" the="" db="" name="" came="" on="" post="" if(isset($_post['db_name'])="" &&="" $_post['db_name']="" !='' ){="" $db_name="$_POST['db_name'];" }else{="" $err="true;" $err_db_name="true;" }="" check="" if="" the="" db="" user="" came="" on="" post="" if(isset($_post['db_user'])="" &&="" $_post['db_user']="" !='' ){="" $db_user="$_POST['db_user'];" }else{="" $err="true;" $err_db_user="true;" }="" check="" if="" the="" db="" user="" password="" came="" on="" post="" if(isset($_post['db_pass'])="" &&="" $_post['db_pass']="" !='' ){="" $db_pass="$_POST['db_pass'];" }="" if(!$err){="" $conn="mysql_connect($db_host," $db_user,="" $db_pass);="" utf8="" mysql_query("set="" character_set_results='utf8' ,="" character_set_client='utf8' ,="" character_set_connection='utf8' ,="" character_set_database='utf8' ,="" character_set_server='utf8' ");="" if(!$conn){="" $err="true;" $err_general_message='Could not connect: ' .="" mysql_errno().="" '="" '.mysql_error().=""?>  
 Check username and password.';
			}else{

				$selected_db = mysql_select_db($db_name);

				if(!$selected_db){
					$err = true;
					$err_general_message = 'Could not select database: '.mysql_errno().' '.mysql_error();
				}else{
					$connected  = true;

					$result = mysql_query('SHOW TABLES');

					while($row = mysql_fetch_row($result))
					{
					  $tables[] = $row[0];
					}

					$return = '';
					foreach($tables as $table){
						$result = mysql_query('SELECT * FROM '.$table);
						$num_fields = mysql_num_fields($result);

						$return.= 'DROP TABLE '.$table.';';
						$row2 = mysql_fetch_row(mysql_query('SHOW CREATE TABLE '.$table));
						$return.= "\n\n".$row2[1].";\n\n";

						for ($i = 0; $i < $num_fields;="" $i++)="" {="" while($row="mysql_fetch_row($result))" {="" $return.='INSERT INTO ' .$table.'="" values(';="" for($j="0;"><$num_fields; $j++)="" {="" $row[$j]="addslashes($row[$j]);" $row[$j]="ereg_replace(" \n","\\n",$row[$j]);"="" if="" (isset($row[$j]))="" {="" $return.='"' .$row[$j].'"'="" ;="" }="" else="" {="" $return.='""' ;="" }="" if=""></$num_fields;><($num_fields-1)) {="" $return.=',' ;="" }="" }="" $return.=");\n" ;="" }="" }="" $return.="\n\n\n" ;="" }="" $handle="fopen($db_name.'-'.date('Y-m-d').'.sql','w+');" fwrite($handle,$return);="" if(fclose($handle)){="" header('content-type:="" application/x-sql');="" header('content-disposition:="" attachment;="" filename="'.urlencode($db_name.'-'.date('Y-m-d').'.sql').'" ');="" header('content-transfer-encoding:="" binary');="" if(readfile($db_name.'-'.date('y-m-d').'.sql')){="" unlink($db_name.'-'.date('y-m-d').'.sql');="" }="" exit;="" }="" }="" }="" }="" }=""></($num_fields-1))>

<style type="text/css">
	body, html, div, ul,li,a  {margin:0; padding:0;}
	body {font-family:arial;font-size:14px;color:#494949;background:#dbdbdb;}
	.clear {clear:both;}
	a img {border:none;}
	h1 {color:#111731;display:inline;}
	#content {width:600px; margin:0 auto;background:#fff;border:1px solid #a2a2a2;margin-top:5px;margin-bottom:20px;}
	#logo {width:600px; margin:0 auto; margin-top:10px; }
	#logo img {vertical-align:middle;}

	#form {width:400px; margin:0 auto;padding:10px;}
	#form label {display:block; width:150px;float:left;margin:13px 0;}
	#form .textField {border:1px solid #ccc;padding:5px; margin:10px 0 10px 20px;color:#494949}

	p.err {padding-left:170px; color:#aa1b1b;}
	p.general_err {text-align:center; background:#aa1b1b;color:#fff;padding:10px;}
	p.general_msg {text-align:center; background:#208118;color:#fff;padding:10px;margin:10px;}
</style>

	<div id="logo">
		[![](http://mihaifrentiu.com/resources/mf_logo_jan_2012.png)](http://mihaifrentiu.com)

# Database backup v0.1

	</div>
	<div id="content">
		<?php if(!$connected){=""?>
		<div id="form">
			<?php if(isset($err_general_message)="" &&="" $err_general_message="" !='' ){=""?>

<?php echo="" $err_general_message;=""?>

			<?php }=""?>
			<form name="db_bkp" method="post">
				<label for="db_host">Host <sub>(in 99% percent of the cases is localhost)</sub></label>
				<input type="text" name="db_host" id="db_host" value="<?php echo (isset($_POST['db_host'])) ? $_POST['db_host'] : 'localhost'; ?>" class="textField">

				<?php if(isset($err_host)="" &&="" $err_host){?=""?>

You must specify the database host.

				<?php }=""?>

				<label for="db_name">Database name</label>
				<input type="text" name="db_name" id="db_name" value="<?php echo (isset($_POST['db_name'])) ? $_POST['db_name'] : ''; ?>" class="textField">

				<?php if(isset($err_db_name)="" &&="" $err_db_name){?=""?>

You must specify the database name.

				<?php }=""?>

				<label for="db_user">Database user</label>
				<input type="text" name="db_user" id="db_user" value="<?php echo (isset($_POST['db_user'])) ? $_POST['db_user'] : ''; ?>" class="textField">

				<?php if(isset($err_db_user)="" &&="" $err_db_user){?=""?>

You must specify the database user.

				<?php }=""?>

				<label for="password">Password</label>
				<input type="password" name="db_pass" id="db_pass" value="" class="textField">

				<input type="submit" class="submitBtn" name="submit" value="Backup Database">
			</form>
		</div>
		<?php }else{=""?>

Backing up database. Please be patient!

		<?php }=""?>

	</div>

```</strong>

origin - http://www.pipiscrew.com/?p=3392 mysql-mysql-backup