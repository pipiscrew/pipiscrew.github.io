---
title: login template
author: PipisCrew
date: 2015-02-07
categories: []
toc: true
---

```js
//admin.html

		<div class="container">
			<div class="alert alert-success" id="alertBOX" style="display:none;"></div>

			<div class="form-signin">
				<form class="form-signin" method="post" action="adminlogin.php">

## Administration

					<input name="email" id="email" type="text" class="form-control" placeholder="Email address" autofocus="">
					<input name="pass" id="pass" type="password" class="form-control" placeholder="Password">
					<label class="checkbox">
						<input type="checkbox" id="rememberCheckbox" value="remember-me">
						Remember me </label>
					<button class="btn btn-lg btn-primary btn-block" type="submit" name="submit" id="login">
						login
					</button>
				</form>
			</div>

		</div>

//signin.css
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
  font-size: 16px;
  height: auto;
  padding: 10px;
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="text"] {
  margin-bottom: -1px;
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
```

```js
//adminlogin.php
<?php session_start();="" if="" (isset($_post['submit']))//if="" the="" form="" has="" been="" submitted="" {="" include="" ('config.php');="" $db="connect();" try="" to="" find="" @="" users="" table="" (aka="" admin/3rd="" party="" users)="" $r="getRow($db," "select="" *="" from="" users="" where="" mail="?" and="" password="?"," array($_post['email'],="" $_post['pass']));="" if="" ($r=""?> 0) {
		date_default_timezone_set("UTC");
		//Login success - set session cookie

		$_SESSION['id'] = $r['user_id'];
//		$_SESSION['level'] = $r['user_level_id'];
//		$_SESSION['login_expiration'] = date("Y-m-d");
//		
//		executeSQL($db,"update users set last_logon=? where user_id=?", array($dt, $user_id));

		//Redirect the user to a logged in page
		header("Location: index.php");

		//Do not display any more script for this page
		exit ;
	} else
			//Redirect the user to login page
			header("Location: admin.html");

} else
	echo "no submit";
?>
```

```js
//index.php
<?php session_start();="" if="" (!isset($_session["id"]))="" {="" header("location:="" index.html");="" exit="" ;="" }=""?>

[Logout](logout.php)

//logout.php
<?php session_start();="" ensure="" you="" are="" using="" same="" session="" session_destroy();="" destroy="" the="" session="" header("location:="" admin.html");="" to="" redirect="" back="" to="" login=""?>
```

more 
http://github.com/CasperGemini/RegistrationForm
http://www.html-form-guide.com/php-form/php-registration-form.html
http://www.html-form-guide.com/php-form/php-login-form.html

origin - http://www.pipiscrew.com/?p=2314 php-login-template