---
title: o[php+mysql] one page login system with password_hash
author: PipisCrew
date: 2015-08-09
categories: [php]
toc: true
---

references
[http://jonsuh.com/blog/securely-hash-passwords-with-php/](http://jonsuh.com/blog/securely-hash-passwords-with-php/)

password_* methods are only available as of PHP 5.5, for older use this instead :
[http://github.com/ircmaxell/password_compat/blob/master/lib/password.php](http://github.com/ircmaxell/password_compat/blob/master/lib/password.php)

**PASSWORD_BCRYPT** uses the CRYPT_BLOWFISH algorithm and will return a <span style="font-size: 30px;">60 character string</span>.
**PASSWORD_DEFAULT** uses the bcrypt algorithm. PHP documentation recommends that you set the column size to 255 in the event the algorithm changes over time.

```js
//one page login system
<?php if="" ($_server['request_method']="==" 'post')="" {="" $password_string="mysql_escape_string($_POST[" upassword"]);"="" include('config.php');="" my="" dbase="" obj="" require('password.php');="" $db="connect();" get="" the="" dbase="" password="" for="" this="" mail="" $password_hash="getScalar($db," select"="" user_password="" from="" users="" where="" user_mail="?" ,array($_post['umail']));"="" ^if="" record="" exists="" if="" ($password_hash){="" if="" (password_verify($password_string,="" $password_hash))="" {="" die("correct");="" }="" else="" {="" die("in-correct");="" }="" }="" else="" {="" user="" doesnt="" exist="" create="" new="" -="" tested&working="" $password_hash="password_hash($password_string," password_bcrypt);="" $sql="INSERT INTO users (user_mail, user_password, user_level) VALUES (:user_mail, :user_password, :user_level)" ;="" $stmt="$db-"?>prepare($sql);

		$stmt->bindValue(':user_mail' , $_POST['umail']);
		$stmt->bindValue(':user_password' , $password_hash);
		$stmt->bindValue(':user_level' , 1);

		$stmt->execute();

		$res = $stmt->rowCount();

		if($res == 1)
			header("Location: http://google.com");
		else
			echo "error";
	}

}
?>

<style>
	body {
	  padding-top: 40px;
	  padding-bottom: 40px;
	  background-color: #eee;
	}

	.form-signin {
	  max-width: 330px;
	  padding: 15px;
	  margin: 0 auto;
	}
	.form-signin .form-signin-heading,
	.form-signin .checkbox {
	  margin-bottom: 10px;
	}
	.form-signin .checkbox {
	  font-weight: normal;
	}
	.form-signin .form-control {
	  position: relative;
	  height: auto;
	  -webkit-box-sizing: border-box;
	     -moz-box-sizing: border-box;
	          box-sizing: border-box;
	  padding: 10px;
	  font-size: 16px;
	}
	.form-signin .form-control:focus {
	  z-index: 2;
	}
	.form-signin input[type="email"] {
	  margin-bottom: -1px;
	  border-bottom-right-radius: 0;
	  border-bottom-left-radius: 0;
	}
	.form-signin input[type="password"] {
	  margin-bottom: 10px;
	  border-top-left-radius: 0;
	  border-top-right-radius: 0;
	}
</style>

			$(function() {
				//pipiscrew
			});

    <div class="container">

      <form class="form-signin" method="POST" action="">

## Please sign in

        <label for="umail" class="sr-only">Email address</label>
        <input type="email" name="umail" class="form-control" placeholder="Email address" required="" autofocus="">
        <label for="upassword" class="sr-only">Password</label>
        <input type="password" name="upassword" id="upassword" class="form-control" placeholder="Password" required="">

        <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
      </form>

    </div> 

```

* * *

[http://www.miraclesalad.com/webtools/md5.php](http://www.miraclesalad.com/webtools/md5.php)
[http://stackoverflow.com/a/704543/1320686](http://stackoverflow.com/a/704543/1320686)

> and why do this^, better use the php md5/sha1 function, the result will be the same

```js
//test_md5.php
<?php @session_start();="" if="" ($_server['request_method']="==" 'post')="" {="" $password_string="md5(mysql_escape_string($_POST[" upassword"]));"="" include('config.php');="" $db="connect();" get="" the="" dbase="" password="" for="" this="" mail="" $r="getRow($db," select"="" user_id,user_level="" from="" users="" where="" user_mail="?" and="" user_password="?" ,array($_post['umail'],"="" $password_string));="" ^if="" record="" exists="" if="" ($r){="" $_session['id']="$r[" user_id"];"="" $_session['level']="$r[" user_level"];"="" header("location:="" portal.php");="" }="" else="" {="" user="" doesnt="" exist="" create="" new="" -="" tested&working="" $sql="INSERT INTO users (user_mail, user_password, user_level) VALUES (:user_mail, :user_password, :user_level)" ;="" $stmt="$db-"?>prepare($sql);

		$stmt->bindValue(':user_mail' , $_POST['umail']);
		$stmt->bindValue(':user_password' , $password_string);
		$stmt->bindValue(':user_level' , 1);

		$stmt->execute();

		$res = $stmt->rowCount();

		if($res == 1)
			header("Location: http://google.com");
		else
			echo "error";
	}
}
?>

<style>
	body {
	  padding-top: 40px;
	  padding-bottom: 40px;
	  background-color: #eee;
	}

	.form-signin {
	  max-width: 330px;
	  padding: 15px;
	  margin: 0 auto;
	}
	.form-signin .form-signin-heading,
	.form-signin .checkbox {
	  margin-bottom: 10px;
	}
	.form-signin .checkbox {
	  font-weight: normal;
	}
	.form-signin .form-control {
	  position: relative;
	  height: auto;
	  -webkit-box-sizing: border-box;
	     -moz-box-sizing: border-box;
	          box-sizing: border-box;
	  padding: 10px;
	  font-size: 16px;
	}
	.form-signin .form-control:focus {
	  z-index: 2;
	}
	.form-signin input[type="email"] {
	  margin-bottom: -1px;
	  border-bottom-right-radius: 0;
	  border-bottom-left-radius: 0;
	}
	.form-signin input[type="password"] {
	  margin-bottom: 10px;
	  border-top-left-radius: 0;
	  border-top-right-radius: 0;
	}
</style>

			$(function() {
				//pipiscrew
			});

    <div class="container">

      <form class="form-signin" method="POST" action="">

## Please sign in

        <label for="umail" class="sr-only">Email address</label>
        <input type="email" name="umail" class="form-control" placeholder="Email address" required="" autofocus="">
        <label for="upassword" class="sr-only">Password</label>
        <input type="password" name="upassword" id="upassword" class="form-control" placeholder="Password" required="">

        <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
      </form>

    </div> 

```

<strong style="color:red">similar** - [https://www.pipiscrew.com/2015/08/phpmysql-password-recovery-via-mail/](https://www.pipiscrew.com/2015/08/phpmysql-password-recovery-via-mail/)</strong>

origin - http://www.pipiscrew.com/?p=3228 php-one-page-login-system