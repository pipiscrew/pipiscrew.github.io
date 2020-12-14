---
title: o[firebase] rules
author: PipisCrew
date: 2017-02-26
categories: [news]
toc: true
---

references :
[ https://www.firebase.com/blog/2013-10-01-queries-part-one.html](https://www.firebase.com/blog/2013-10-01-queries-part-one.html)
[ https://www.firebase.com/blog/2014-01-02-queries-part-two.html](https://www.firebase.com/blog/2014-01-02-queries-part-two.html)
[https://www.firebase.com/blog/2013-08-01-new-feature-improved-string-validation-in-security-rules.html](https://www.firebase.com/blog/2013-08-01-new-feature-improved-string-validation-in-security-rules.html)
[https://www.firebase.com/docs/security/rulesdatasnapshot/index.html](https://www.firebase.com/docs/security/rulesdatasnapshot/index.html)
[https://gist.github.com/katowulf/4741111](https://gist.github.com/katowulf/4741111)
[https://gist.github.com/katowulf/6158392](https://gist.github.com/katowulf/6158392)

**when**

```js
{
    "rules": {
     //when
        ".read": true,
        ".write": true,

//this rule doesnt take place!
       "categories": {
        ".read": true,
        ".write": "auth.email == 'x@x.net'" //only super admin can write
    }

    }
}
```

**when**

![](https://www.pipiscrew.com/wp-content/uploads/2014/01/snap453.png "snap453")

and we like each user read+write only to his key

```js
      "companies" : {
        "$user": {
        ".read": "$user == auth.id", //user can read his record only
        ".write": "$user == auth.id" //user can write his record only
        }
      },
```

and superadmin manipulate all records

```js
      "companies" : {
            //only super admin can read/write anything in companies
            ".read": "auth.email == 'x@x.net'",
            ".write": "auth.email == 'x@x.net'",

        "$user": {
              ".read": "$user == auth.id", //user can read his record only
              ".write": "$user == auth.id" //user can write his record only
        }
      },
```

**when**

![](https://www.pipiscrew.com/wp-content/uploads/2014/01/snap457.png "snap457")

only super admin writes at red rectangle, users can create node only in **comp** node and must contains **adminID**, also when editing the record inside **comp**, the rule checks that current logged **userID** equals with **adminID** field!

**WARNING** when make transaction with **<span style="color: #ff0000;">Firebase</span>** the **adminID** field must be <span style="color: #ff0000;">**text**</span> otherwise cant compare it!

```js
       "categories": {
            ".read": true,
            ".write": "auth.email == 'x@x.net'",

            "$catKeyID": {
                  ".read": true,
                  ".write": "false",

              "comp": {
                  ".read": true,
                  ".write": false ,

                "$compKeyID": {
                                  ".validate": "(data.exists() && data.child('adminID').val()==auth.id) || (!data.exists() && newData.child('adminID').val()==auth.id)",
                                  ".read": true,
                                  ".write": true
                              }
              },
            }
    }
```

origin - http://www.pipiscrew.com/?p=652 firebase-rules