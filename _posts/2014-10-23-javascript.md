---
title: o[javascript] login with facebook
author: PipisCrew
date: 2014-10-23
categories: []
toc: true
---

reference [http://developers.facebook.com/docs/facebook-login/login-flow-for-web/v2.1](http://developers.facebook.com/docs/facebook-login/login-flow-for-web/v2.1)

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap106.png "snap106")
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap107.png "snap107")

**write down the appid**
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap108.png "snap108")

fill out, all red rects :
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap109.png "snap109")
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap110.png "snap110")
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap111.png "snap111")

then a html :
```js

  // This is called with the results from from FB.getLoginStatus().
  function statusChangeCallback(response) {
    console.log('statusChangeCallback');
    console.log(response);
    // The response object is returned with a status field that lets the
    // app know the current login status of the person.
    // Full docs on the response object can be found in the documentation
    // for FB.getLoginStatus().
    if (response.status === 'connected') {
      // Logged into your app and Facebook.
      testAPI();
    } else if (response.status === 'not_authorized') {
      // The person is logged into Facebook, but not your app.
      document.getElementById('status').innerHTML = 'Please log ' +
        'into this app.';
    } else {
      // The person is not logged into Facebook, so we're not sure if
      // they are logged into this app or not.
      document.getElementById('status').innerHTML = 'Please log ' +
        'into Facebook.';
    }
  }

  // This function is called when someone finishes with the Login
  // Button.  See the onlogin handler attached to it in the sample
  // code below.
  function checkLoginState() {
    FB.getLoginStatus(function(response) {
      statusChangeCallback(response);
    });
  }

  window.fbAsyncInit = function() {
  FB.init({
    appId      : 'you appID,
    cookie     : true,  // enable cookies to allow the server to access 
                        // the session
    xfbml      : true,  // parse social plugins on this page
    version    : 'v2.1' // use version 2.1
  });

  // Now that we've initialized the JavaScript SDK, we call 
  // FB.getLoginStatus().  This function gets the state of the
  // person visiting this page and can return one of three states to
  // the callback you provide.  They can be:
  //
  // 1. Logged into your app ('connected')
  // 2. Logged into Facebook, but not your app ('not_authorized')
  // 3. Not logged into Facebook and can't tell if they are logged into
  //    your app or not.
  //
  // These three cases are handled in the callback function.

  FB.getLoginStatus(function(response) {
    statusChangeCallback(response);
  });

  };

  // Load the SDK asynchronously
  (function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s); js.id = id;
    js.src = "//connect.facebook.net/en_US/sdk.js";
    fjs.parentNode.insertBefore(js, fjs);
  }(document, 'script', 'facebook-jssdk'));

  // Here we run a very simple test of the Graph API after login is
  // successful.  See statusChangeCallback() for when this call is made.
  function testAPI() {
    console.log('Welcome!  Fetching your information.... ');
    FB.api('/me', function(response) {
    	console.log(response);
      console.log('Successful login for: ' + response.name);
      document.getElementById('status').innerHTML =
        'Thanks for logging in, ' + response.name + '!';
    });
  }

	<div style="text-align: center; width: 100%;">
		![](img/banner.jpg)  

		<div class="fb-login-button" data-max-rows="1" data-size="xlarge" data-show-faces="false" data-auto-logout-link="true" scope="public_profile,email" data-size="xlarge" onlogin="checkLoginState();">
		</div>

		<div id="status">
		</div>
	</div>

<!--<fb:login-button scope="public_profile,email" data-size="xlarge" onlogin="checkLoginState();">
</fb:login-button>-->

```

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap112.png "snap112")

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap113.png "snap113")

origin - http://www.pipiscrew.com/?p=1592 javascript-login-with-facebook