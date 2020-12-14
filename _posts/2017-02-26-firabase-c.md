---
title: o[firabase] custom login via PHP + read nodes
author: PipisCrew
date: 2017-02-26
categories: [Uncategorized]
toc: true
---

references :

Firebase Custom Login -  [https://www.firebase.com/docs/security/custom-login.html](https://www.firebase.com/docs/security/custom-login.html)

Firebase REST API -  [https://www.firebase.com/docs/rest-api.html](https://www.firebase.com/docs/rest-api.html)

Firebase Token Generator for PHP - [https://github.com/firebase/firebase-token-generator-php](https://github.com/firebase/firebase-token-generator-php)

Encode and decode JSON Web Tokens (JWT) in PHP - [https://github.com/firebase/php-jwt](https://github.com/firebase/php-jwt)

Firebase PHP Helper Library - [https://github.com/ktamas77/firebase-php](https://github.com/ktamas77/firebase-php)

# 1-

upload to server **FirebaseToken.php** + **JWT.php + firebaseLib.php**

# 2-

```js
<?php include_once="" "firebasetoken.php";="" require_once="" 'firebaselib.php';="" $secret="dHQkvze--" ;="" firebase="" secret="" $tokengen="new" services_firebasetokengenerator($secret);="" $token="$tokenGen" -=""?> createToken(array("app_user_id" => 1234, "isAdmin" => true));

$url = 'https://x.firebaseio.com/';

$fb = new fireBase($url, $token);

$response = $fb -> get('/debugNode/');
//echo $response;  //using firebaseLib by default is json, no need to use 'REST API' .json

$jsonArray = json_decode($response);

$tmp = "";
foreach ($jsonArray as $value) {
	$debugChildNode = $value; //node

	$tmp .= $debugChildNode -> Comment . "  
"; //field
}

echo $tmp;

?>
```

the rule :

```js
       "debugNode": { 
                   ".read": "auth.isAdmin == true", 
                   ".write": "auth.isAdmin == true"
       } 
```

origin - http://www.pipiscrew.com/?p=716 firabase-custom-login-via-php