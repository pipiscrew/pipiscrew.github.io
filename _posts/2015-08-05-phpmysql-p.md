---
title: o[php+mysql] password recovery via mail
author: PipisCrew
date: 2015-08-05
categories: []
toc: true
---

**login_forgot.php**
```js
//login_forgot.php

<div class="container-fluid">
	<div class="row" style="overflow: auto;background-color: #af156b;border-bottom:2px #eee solid">
		<div class="container" style="padding-top: 3px;">
			![](assets/img/facebook.png)
			![](assets/img/google.png)
			![](assets/img/in.png)
			![](assets/img/twitter.png)
			![](assets/img/youtube.png)
		</div>
	</div>
</div>  

	<div class="container">

<?php @session_start();="" include('config.php');="" $db="connect();" if="" ($_server['request_method']="==" 'post')="" {="" $boundary="urlencode(uniqid(rand()," true));="" $user_mail="mysql_escape_string($_POST[" email"]);"="" $member_id="getScalar($db," "select="" member_id="" from="" members="" where="" email="?" ,array($user_mail));"="" if="" ($member_id)="" {="" $id="intval($member_id);" if="" ($id=""?>0)
		{
			executeSQL($db, "update members set password_recovery_key=? where member_id=?",array($boundary, $member_id));

			$user_mail="x@x.com";
			if (sendMail($user_mail,"PipisCrew Password Reset","[Click here to reset your password](http://www.x.com/login_forgot.php?l=".$boundary."&action=reset)"))
			{	echo "<div class='alert alert-success'>An email sent to {$user_mail}</div>";
				exit;
			}
			else
				echo "<div class='alert alert-danger'>An error occured when tried to send an email to {$user_mail}, please try again</div>" ;
		}
	}
	else 
		echo "  
<div class='alert alert-danger'>Could not find any user with email {$user_mail}, please try again!</div>  
" ;
} elseif ($_SERVER['REQUEST_METHOD'] === 'GET') {

	if (isset($_GET["l"]) && !empty($_GET["l"]) && isset($_GET["action"]) && !empty($_GET["action"]))
	{
		if (!getScalar($db, "select member_id from members where password_recovery_key=?",array($_GET["l"])))
		{
			unset($_SESSION["pass_boundary"]); //if any?

			die("<div class='container'><div class='alert alert-danger'>An error occured! 0x3s45</div></div>");
		}

	$_SESSION["pass_boundary"] = $_GET["l"];	
	?>

		<form id="form_forgot" method="post" action="login_reset.php" onsubmit="if (document.getElementsByName('password1')[0].value != document.getElementsByName('password2')[0].value) alert('password fields not match'); return document.getElementsByName('password1')[0].value == document.getElementsByName('password2')[0].value;">

				<div class="form-group">
					<label>Enter new password :</label>
					<input name="password1" maxlength="60" type="text" class="form-control" placeholder="password" required="">
				</div>

				<div class="form-group">
					<label>Re-type new password :</label>
					<input name="password2" maxlength="60" type="text" class="form-control" placeholder="Re-type new password" required="">
				</div>

				<center><button class="btn btn-primary btn-sm" type="submit">Save new password</button></center>
		</form>

<?php exit;}="" }="" function="" sendmail($recipient_mail,="" $subject,="" $body)="" {="" $headers="From: report@x.com\r\n" ;="" $headers="" .="MIME-Version: 1.0\r\n" ;="" $headers="" .="Content-Type: text/html; charset=utf-8\r\n" ;="" $message='' ;="" $message="" .="$body;" $message="" .='' ;="" line="" with="" trick="" -="" http://www.xpertdeveloper.com/2013/05/set-unicode-character-in-email-subject-php/="" $updated_subject="=?UTF-8?B?" .="" base64_encode($subject)="" .="" "?=";

    if (mail($recipient_mail, $updated_subject, $message, $headers)) {
      return true;
    } else {
      return false;
    }
}
?>

		<form id=" form_forgot"="" method="post"?>

				<div class="form-group">
					<label>Email :</label>
					<input name="email" maxlength="100" type="email" class="form-control" placeholder="Email" required="">
				</div>

				<center><button class="btn btn-primary btn-sm" type="submit">Send Password Reset</button></center>
		</form>
	</div>

```

**login_reset.php**
```js
//login_reset.php

<div class="container-fluid">
	<div class="row" style="overflow: auto;background-color: #af156b;border-bottom:2px #5d5d5d solid">
		<div class="container" style="padding-top: 3px;">
			![](assets/img/facebook.png)
			![](assets/img/google.png)
			![](assets/img/in.png)
			![](assets/img/twitter.png)
			![](assets/img/youtube.png)
		</div>
	</div>
</div>  

	<div class="container">

<?php @session_start();="" if="" (!isset($_session["pass_boundary"])="" ||="" !isset($_post["password1"])="" ||="" !isset($_post["password2"]))="" {="" header("location:="" index.php");="" exit="" ;="" }="" include('config.php');="" $db="connect();" $boundary="$_SESSION[" pass_boundary"];"="" $member_id="getScalar($db," "select="" member_id="" from="" members="" where="" password_recovery_key="?" ,array($boundary));"="" if($member_id){="" $password_string="md5(mysql_escape_string($_POST[" password1"]));"="" executesql($db,="" "update="" members="" set="" password="?," password_recovery_key="null" where="" member_id="?" ,array($password_string"="" ,="" $member_id));="" echo=""?><div class='container'><div class='alert alert-success'>The password changed! Please try to login now!</div></div>";
}
else 
	echo "  
<div class='container'><div class='alert alert-danger'>Could not find the user defined!, please try again!</div></div>  
" ;

 unset($_SESSION["pass_boundary"]);
?>
</div>

```

```js
CREATE TABLE members (
  member_id int(11) NOT NULL AUTO_INCREMENT,
  email varchar(50) COLLATE utf8_unicode_ci DEFAULT NULL,
  password varchar(60) COLLATE utf8_unicode_ci DEFAULT NULL,
  password_recovery_key varchar(35) CHARACTER SET utf8 DEFAULT '',
  PRIMARY KEY (member_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```

origin - http://www.pipiscrew.com/?p=3585 phpmysql-password-recovery-via-mail