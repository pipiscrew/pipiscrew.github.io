---
title: login with facebook
author: PipisCrew
date: 2014-10-27
categories: []
toc: true
---

reference
[https://www.webniraj.com/2014/05/01/facebook-api-php-sdk-updated-to-v4-0-0/](https://www.webniraj.com/2014/05/01/facebook-api-php-sdk-updated-to-v4-0-0/)

download FacebookSDK by [http://github.com/facebook/facebook-php-sdk-v4](http://github.com/facebook/facebook-php-sdk-v4)
at the time of article is <span style="color: #ff0000;">**v4.0.11**</span>

create a FacebookApp as described here [https://www.pipiscrew.com/2014/10/javascript-login-with-facebook/](https://www.pipiscrew.com/2014/10/javascript-login-with-facebook/)

plus fill out the website URL

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap114.png "snap114")

plus enable **App Secret Proof for Server API calls** more at  [http://developers.facebook.com/docs/graph-api/securing-requests/](http://developers.facebook.com/docs/graph-api/securing-requests/)

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap115.png "snap115")

upload the Facebook folder by **facebook-php-sdk-v4-4.0-dev.zip\facebook-php-sdk-v4-4.0-dev\src**

create a login.php as the following :

```js
<?php require_once(="" 'facebook/httpclients/facebookhttpable.php'="" );="" require_once(="" 'facebook/httpclients/facebookcurl.php'="" );="" require_once(="" 'facebook/httpclients/facebookcurlhttpclient.php'="" );="" require_once(="" 'facebook/entities/accesstoken.php'="" );="" require_once(="" 'facebook/entities/signedrequest.php'="" );="" require_once(="" 'facebook/facebooksession.php'="" );="" require_once(="" 'facebook/facebookredirectloginhelper.php'="" );="" require_once(="" 'facebook/facebookrequest.php'="" );="" require_once(="" 'facebook/facebookresponse.php'="" );="" require_once(="" 'facebook/facebooksdkexception.php'="" );="" require_once(="" 'facebook/facebookrequestexception.php'="" );="" require_once(="" 'facebook/facebookotherexception.php'="" );="" require_once(="" 'facebook/facebookauthorizationexception.php'="" );="" require_once(="" 'facebook/graphobject.php'="" );="" require_once(="" 'facebook/graphsessioninfo.php'="" );="" use="" facebook\httpclients\facebookhttpable;="" use="" facebook\httpclients\facebookcurl;="" use="" facebook\httpclients\facebookcurlhttpclient;="" use="" facebook\entities\accesstoken;="" use="" facebook\entities\signedrequest;="" use="" facebook\facebooksession;="" use="" facebook\facebookredirectloginhelper;="" use="" facebook\facebookrequest;="" use="" facebook\facebookresponse;="" use="" facebook\facebooksdkexception;="" use="" facebook\facebookrequestexception;="" use="" facebook\facebookotherexception;="" use="" facebook\facebookauthorizationexception;="" use="" facebook\graphobject;="" use="" facebook\graphsessioninfo;="" start="" session="" session_start();="" init="" app="" with="" app="" id="" and="" secret="" facebooksession::setdefaultapplication('appid','secret');="" login="" helper="" with="" redirect_uri="" $helper="new" facebookredirectloginhelper('http://x.com/testfb/playground_admin/login.php');="" see="" if="" a="" existing="" session="" exists="" if="" (="" isset(="" $_session="" )="" &&="" isset(="" $_session['fb_token']="" )="" )="" {="" create="" new="" session="" from="" saved="" access_token="" $session="new" facebooksession(="" $_session['fb_token']="" );="" validate="" the="" access_token="" to="" make="" sure="" it's="" still="" valid="" try="" {="" if="" (="" !$session-=""?>validate() ) {
      $session = null;
    }
  } catch ( Exception $e ) {
    // catch any exceptions
    $session = null;
  }
}  

if ( !isset( $session ) || $session === null ) {
  // no session exists

  try {
    $session = $helper->getSessionFromRedirect();
  } catch( FacebookRequestException $ex ) {
    // When Facebook returns an error
    // handle this better in production code
    print_r( $ex );
  } catch( Exception $ex ) {
    // When validation fails or other local issues
    // handle this better in production code
    print_r( $ex );
  }

}

// see if we have a session
if ( isset( $session ) ) {

  // save the session
  $_SESSION['fb_token'] = $session->getToken();
  // create a session using saved token or the new one we generated at login
  $session = new FacebookSession( $session->getToken() );

  // graph api request for user data
  $request = new FacebookRequest( $session, 'GET', '/me' );
  $response = $request->execute();
  // get response
  $graphObject = $response->getGraphObject()->asArray();

  // print profile data
  echo '

' . print_r( $graphObject,1) . '
';

  // print logout url using session and redirect_uri (logout.php page should destroy the session)
  echo '[Logout](' . $helper->getLogoutUrl( $session, 'http://x.com/testFB/playground_admin/logout.php' ) . ')';

} else {
  // show login url - ask for permissions email + user_friends
  echo '[Login](' . $helper->getLoginUrl( array('email', 'user_friends') ) . ')';
}
```

create a logout.php as the following :
```js
<?php session_start();="" to="" ensure="" you="" are="" using="" same="" session="" logout="" session_destroy();="" destroy="" the="" session="" header("location:="" login.php");="" to="" redirect="" back="" to="" login=""?>
```

line **95** :
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap125.png "snap125")

origin - http://www.pipiscrew.com/?p=1611 php-login-with-facebook