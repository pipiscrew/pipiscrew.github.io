---
title: o[firebase] custom login via nodeJS
author: PipisCrew
date: 2017-02-26
categories: [news]
toc: true
---

install

[https://github.com/firebase/firebase-token-generator-node](https://github.com/firebase/firebase-token-generator-node) <span style="color: #0000ff;">(following example using this)</span>

other :
[https://github.com/firebase/firebase-simple-login/](https://github.com/firebase/firebase-simple-login/)

[http://runnable.com/UnGfya9x5Kh2AABy/deconstruct-a-jwt-token-for-firebase-for-javascript](http://runnable.com/UnGfya9x5Kh2AABy/deconstruct-a-jwt-token-for-firebase-for-javascript)

**at nodeJS** script :

```js
    var FirebaseTokenGenerator = require("firebase-token-generator");
    var tokenGenerator = new FirebaseTokenGenerator("firebase-secret-here"); //see picture
    var token = tokenGenerator.createToken({"app_user_id": 1234, "isModerator": true });

    var db = new Firebase('https://' + baseURL);

		db.auth(token, function(error) {
		  if(error) {
		    console.log("Login Failed!", error);
		  } else {
		    console.log("Login Succeeded!");
		  }
		});

    db = new Firebase('https://' + baseURL + '/debug/');
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/01/snap462.png "snap462")

**at Rule**

```js
       "debug": {
                   ".read": "auth.isModerator == true",
                   ".write": "auth.isModerator == true",
                    }
```

origin - http://www.pipiscrew.com/?p=676 firebase-custom-login-via-nodejs