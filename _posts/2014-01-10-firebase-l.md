---
title: o[firebase] logout user
author: PipisCrew
date: 2014-01-10
categories: []
toc: true
---

```js
				//logout
				$("#logout").on('click', function(e) {
					var firebaseRef = new Firebase("https://" + baseURL);

					var auth = new FirebaseSimpleLogin(firebaseRef, function(error, user) {
						if (error | user === null)
							window.location = "index.html";
						else
							auth.logout();
					});
				});
```

origin - http://www.pipiscrew.com/?p=650 firebase-logout-user