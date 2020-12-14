---
title: Converting release key to debug
author: PipisCrew
date: 2014-01-23
categories: []
toc: true
---

**on a MAC :**

[http://blogprogramistyandroid.blogspot.com/2011/04/converting-release-keys-to-debug.html](http://blogprogramistyandroid.blogspot.gr/2011/04/converting-release-keys-to-debug.html)

writes

> keytool -importkeystore -v -srckeystore release.keystore -destkeystore custom-debug.keystore -srcstorepass release-pass -deststorepass android -srcalias release-key -destalias androiddebugkey -srckeypass release-pass -destkeypass android

**on a PC** successfully converted and verified, I created a release

![](https://www.pipiscrew.com/wp-content/uploads/2014/01/Snap565.png "Snap565")

when asked I created a new keystore name it **test.keystore** (+ a new key) I store it under **d:\thisisatest**, you have to write down the **Alias** given to key^ when creating!
Keep in mind that by default the debug keystore/key is under file :

> C:\Users\username\.android\debug.keystore

running the following command from DOS prompt (from C:\Program Files\Java\jre7\bin) :

keytool -importkeystore -v -srckeystore "d:\thisisatest\test.keystore" -destkeystore "d:\thisisatestDEBUG\debug.keystore" -srcstorepass <span style="color: #ff0000;">yourkeystorepassword</span> -deststorepass android -srcalias <span style="color: #ff0000;">alias</span>  -destalias androiddebugkey -srckeypass <span style="color: #ff0000;">yourkeypassword</span> -destkeypass android

so now I have a debug key that has the same private/public key as my release key!!! to verify it go to

Windows -> Preferences -> Android - > Build

![](https://www.pipiscrew.com/wp-content/uploads/2014/01/snap566.png "snap566")

has the same MD5/SHA1 with release keystore!!

origin - http://www.pipiscrew.com/?p=741 android-converting-release-key-to-debug