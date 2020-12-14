---
title: using facebook SDK to call Graph API / FQL Query
author: PipisCrew
date: 2015-04-15
categories: []
toc: true
---

reference 
http://developers.facebook.com/docs/facebook-login/access-tokens
http://developers.facebook.com/docs/php/FacebookSession/4.0.0
http://developers.facebook.com/docs/graph-api/reference/v2.3/post
http://metah.ch/blog/2014/05/facebook-sdk-4-0-0-for-php-a-working-sample-to-get-started/
http://www.sammyk.me/facebook-sdk-v4-for-php-what-you-need-to-know
http://www.sammyk.me/access-token-handling-best-practices-in-facebook-php-sdk-v4

> facebook writes  :
> 
> Version 2.0 of the Facebook Platform API is the last version where FQL will be available. Versions after 2.0 will not support FQL. Please migrate your applications to use Graph API instead of FQL. Please see our changelog for current version information.

First we create an app, going [http://developers.facebook.com](http://developers.facebook.com)

![](https://www.pipiscrew.com/wp-content/uploads/2015/04/snap646.png "snap646")

App access tokens are used to make requests to Facebook APIs **on behalf of an app** rather than a user. This can be used to modify the parameters of your app, create and manage test users, or read your application's insights. App access tokens can also be used to publish content to Facebook on behalf of a person who has granted an open graph publishing permission to your application. source [http://developers.facebook.com/docs/facebook-login/access-tokens#apptokens](http://developers.facebook.com/docs/facebook-login/access-tokens#apptokens)

we go to 
[http://developers.facebook.com/tools/explorer/](http://developers.facebook.com/tools/explorer/)

the GET should be 
```js
/oauth/access_token?
     client_id={app-id}
    &client_secret={app-secret}
    &grant_type=client_credentials
```

so by my app created on start I execute the railway :
![](https://www.pipiscrew.com/wp-content/uploads/2015/04/snap644.png "snap644")

this access_token  is my #**App Access Token**#

write it down!

on a php file + using **facebook-php-sdk-v4-4.0-dev** by [http://github.com/facebook/facebook-php-sdk-v4](http://github.com/facebook/facebook-php-sdk-v4)

```js
//test.php
<?php require_once="" 'facebook/autoload.php';="" use="" facebook\facebookrequest;="" use="" facebook\facebooksession;="" init="" app="" with="" app="" id="" and="" secret="" facebooksession::setdefaultapplication('app-id',="" 'app-secret');="" if="" you="" already="" have="" a="" valid="" access="" token:="" $session="new" facebooksession('app-access-token');="" if="" you're="" making="" app-level="" requests:="" $session="FacebookSession::newAppSession();" your="" graph="" query="" here="" $request="new" facebookrequest(="" $session,="" 'get',="" '/4u4/likes?limit="1000&summary=true'" );="" facebook="" restrict="" the="" size="" of="" query="" to="" 1000="" records="" using="" pagination="" $response="$request-"?>execute();
	$graphObject = $response->getGraphObject();

	echo '

' . print_r($graphObject,1) . '
';
```

with limit=1000
![](https://www.pipiscrew.com/wp-content/uploads/2015/04/snap647.png "snap647")

w/o limit (the default)
![](https://www.pipiscrew.com/wp-content/uploads/2015/04/snap648.png "snap648")

* * *

source [http://stackoverflow.com/a/23528364](http://stackoverflow.com/a/23528364)
doing the same but not use app_token, the app must be accepted by user level then do anything else (run it by login.php) :

```js
//index.php
<?php session_start();="" require_once="" 'facebook/autoload.php';="" use="" facebook\facebookrequest;="" use="" facebook\facebooksession;="" use="" facebook\facebookredirectloginhelper;="" init="" app="" with="" app="" id="" and="" secret="" facebooksession::setdefaultapplication('app-id',="" 'app-secret');="" login="" helper="" with="" redirect_uri="" $helper="new" facebookredirectloginhelper('http://x.com/fbphpcomplete/index.php');="" $session="$helper-"?>getSessionFromRedirect();

	$request = new FacebookRequest(
	  $session,
	  'GET',
	  '/4u4/limit=1000&summary=true'
	);

	$response = $request->execute();
	$graphObject = $response->getGraphObject();

	echo '

' . print_r($graphObject,1) . '
';
?>

//login.php
<?php session_start();="" require="" 'facebook/autoload.php';="" use="" facebook\facebooksession;="" use="" facebook\facebookredirectloginhelper;="" facebooksession::setdefaultapplication('app-id',="" 'app-secret');="" $helper="new" facebookredirectloginhelper('http://x.com/fbphpcomplete/index.php');="" $loginurl="$helper-"?>getLoginUrl();

	echo '[Log In](' . $loginUrl . ')';
?>
```

* * *

Graph API call with old Facebook SDK [http://github.com/facebookarchive/facebook-php-sdk](http://github.com/facebookarchive/facebook-php-sdk)

```js
//test with old facebook SDK
<?php session_start();="" include="" the="" facebook="" sdk="" require_once('resources/facebook-php-sdk-master/src/facebook.php');="" connect="" to="" app="" $config="array();" $config['appid']='app-id' ;="" $config['secret']='app-secret' ;="" $config['fileupload']="false;" optional="" instantiate="" $facebook="new" facebook($config);="" $pagefeed="$facebook-"?>api("/4u4/likes?limit=1300&summary=true");

  	echo '

' . print_r($pagefeed,1) . '
';
```

* * *

> You can use summary when querying a feed or multiple posts. Specify this in the fields parameter.

source - [http://stackoverflow.com/a/18351526](http://stackoverflow.com/a/18351526)

```jshttps://graph.facebook.com/PAGE_ID/feed?fields=comments.limit(1).summary(true),likes.limit(1).summary(true)

This will return a response like this.

{
  "data": [
    {
      ....
      "summary": {
        "total_count": 56
      }
      ...
    }, 
    {
      ....
      "summary": {
        "total_count": 88
      }
      ...
    }
  ]
}
```

* * *

FQL example - Get how many shares/likes/comments made for a specific post

![](https://www.pipiscrew.com/wp-content/uploads/2015/04/snap649.png "snap649")

> https://www.facebook.com/PAGE_ID/posts/POST_ID

```js
// source - http://stackoverflow.com/a/21229441
SELECT like_info.like_count, comment_info.comment_count, share_count 
  FROM stream 
 WHERE post_id = "632261416828769_808723242515918"
```

origin - http://www.pipiscrew.com/?p=2848 php-using-facebook-sdk-to-call-graph-api-fql-query