---
title: o[google-php] OAuth2 by GoogleAPI v3
author: PipisCrew
date: 2014-09-22
categories: []
toc: true
---

[http://developers.google.com/accounts/docs/OAuth2](http://developers.google.com/accounts/docs/OAuth2)
[ http://20missionglass.tumblr.com/post/60787835108/programming-an-oauth2-client-app-in-php](http://20missionglass.tumblr.com/post/60787835108/programming-an-oauth2-client-app-in-php)
[ http://www.lornajane.net/posts/2012/using-oauth2-for-google-apis-with-php](http://www.lornajane.net/posts/2012/using-oauth2-for-google-apis-with-php)
[ http://weblessons.info/2014/06/21/log-in-with-google-tutorial-php/](http://weblessons.info/2014/06/21/log-in-with-google-tutorial-php/)

1-
we creating a new project
[http://console.developers.google.com/project](http://console.developers.google.com/project)
2-
enable the API's we would like to 'play'
![](https://www.pipiscrew.com/wp-content/uploads/2014/09/Snap28.png "Snap28")
3-
we set OAuth credentials
[![](https://www.pipiscrew.com/wp-content/uploads/2014/09/snap028.png "snap028")](https://www.pipiscrew.com/wp-content/uploads/2014/09/snap028.png)
4-
create a API key (this will be used at front, you will understand below)
![](https://www.pipiscrew.com/wp-content/uploads/2014/09/Snap31.png "Snap31")
5-
so are as :
![](https://www.pipiscrew.com/wp-content/uploads/2014/09/snap029.png "snap029")

6-
last thing to set :
![](https://www.pipiscrew.com/wp-content/uploads/2014/09/Snap33.png "Snap33")
otherwise there will be error like :
invalid_client no application name
invalid_client no support email
illustrated
![](https://www.pipiscrew.com/wp-content/uploads/2014/09/Snap34.png "Snap34")

7-
download GoogleSDK-PHP
[http://github.com/google/google-api-php-client](http://github.com/google/google-api-php-client)

we upload the **Google** folder where is inside **src** root folder, into **ftp://.com/oauth2callback** folder so in the end will have **ftp://.com/oauth2callback/Google**

![](https://www.pipiscrew.com/wp-content/uploads/2014/09/snap030.png "snap030")

we create the **ftp://.com/oauth2callback/index.php** 

```js
<?php session_start();="" require_once="" 'google/client.php';="" require_once="" 'google/service/oauth2.php';="" $clientid="20...72-4ma....s6...apps.googleusercontent.com" ;="" $clientsecret="2...........M" ;="" $redirecturi="http://thefacedisplay.com/oauth2callback/index.php" ;="" $client="new" google_client();="" $client---=""?>setScopes(array(
  "https://www.googleapis.com/auth/plus.me",
  "https://www.googleapis.com/auth/userinfo.email"
));

$google_oauthV2 = new Google_Service_Oauth2($client);
$client->setRedirectUri($RedirectUri);
$client->setClientId($ClientId);
$client->setClientSecret($ClientSecret);

// If user is authenticated by Google
if (isset($_REQUEST['code'])) {
//    header('Location: ./index.php');
}
else{
    // Failed Authentication
    if (isset($_REQUEST['error'])) {
        echo "error auth";
    }
    else{
        // Redirects to google for User Authentication
        $authUrl = $client->createAuthUrl();
        header("Location: $authUrl");
    }
}

?>
```

8-

anywhere in your host create a html file as :

```js

<!--   Copyright (c) 2011 Google Inc.   Licensed under the Apache License, Version 2.0 (the "License"); you may not   use this file except in compliance with the License. You may obtain a copy of   the License at   http://www.apache.org/licenses/LICENSE-2.0   Unless required by applicable law or agreed to in writing, software   distributed under the License is distributed on an "AS IS" BASIS, WITHOUT   WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the   License for the specific language governing permissions and limitations under   the License.   To run this sample, replace YOUR API KEY with your application's API key.   It can be found at https://code.google.com/apis/console/?api=plus under API Access.   Activate the Google+ service at https://code.google.com/apis/console/ under Services -->

 <button id="authorize-button" style="visibility: hidden;">Authorize</button>

      // Enter a client ID for a web application from the Google Developer Console.
      // The provided clientId will only work if the sample is run directly from
      // https://google-api-javascript-client.googlecode.com/hg/samples/authSample.html
      // In your Developer Console project, add a JavaScript origin that corresponds to the domain
      // where you will be running the script.
      var clientId = '20...72-4ma....s6..c.apps.googleusercontent.com';

      // Enter the API key from the Google Develoepr Console - to handle any unauthenticated
      // requests in the code.
      // The provided key works for this sample only when run from
      // https://google-api-javascript-client.googlecode.com/hg/samples/authSample.html
      // To use in your own application, replace this API key with your own.
      var apiKey = 'AI...ZyepE7TW8';

      // To enter one or more authentication scopes, refer to the documentation for the API.
      var scopes = 'https://www.googleapis.com/auth/plus.me';

      // Use a button to handle authentication the first time.
      function handleClientLoad() {
        gapi.client.setApiKey(apiKey);
        window.setTimeout(checkAuth,1);
      }

      function checkAuth() {
        gapi.auth.authorize({client_id: clientId, scope: scopes, immediate: true}, handleAuthResult);
      }

      function handleAuthResult(authResult) {
        var authorizeButton = document.getElementById('authorize-button');
        if (authResult && !authResult.error) {
          authorizeButton.style.visibility = 'hidden';
          makeApiCall();
        } else {
          authorizeButton.style.visibility = '';
          authorizeButton.onclick = handleAuthClick;
        }
      }

      function handleAuthClick(event) {
        gapi.auth.authorize({client_id: clientId, scope: scopes, immediate: false}, handleAuthResult);
        return false;
      }

      // Load the API and make an API call.  Display the results on the screen.
      function makeApiCall() {
        gapi.client.load('plus', 'v1', function() {
          var request = gapi.client.plus.people.get({
            'userId': 'me'
          });
          request.execute(function(resp) {
            var heading = document.createElement('h4');
            var image = document.createElement('img');
            image.src = resp.image.url;
            heading.appendChild(image);
            heading.appendChild(document.createTextNode(resp.displayName));

            document.getElementById('content').appendChild(heading);
          });
        });
      }

```

9-
now when navigate to this html^ when click authorize will be like

[![](https://www.pipiscrew.com/wp-content/uploads/2014/09/snap031.png "snap031")](https://www.pipiscrew.com/wp-content/uploads/2014/09/snap031.png)

Javascript OAuth and REST library - [http://adodson.com/hello.js](http://adodson.com/hello.js)

google-oauth2-web-client - [http://github.com/timdream/google-oauth2-web-client ](http://github.com/timdream/google-oauth2-web-client )

> Why not use library supplied by Google and reinvent the wheel?
> Because I can; also because the library is light-weighted and transparent to me. For some reason, I cannot get auth library to load without getting the entire client library; onload callback never fires.
> You are very welcome to use the library from Google since it will be better supported.

origin - http://www.pipiscrew.com/?p=1353 google-php-oauth2-by-googleapi-v3