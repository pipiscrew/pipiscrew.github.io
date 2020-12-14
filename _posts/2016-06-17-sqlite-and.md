---
title: SQLite and Android N
author: PipisCrew
date: 2016-06-17
categories: [android]
toc: true
---

The SQLite library that comes with Android is actually not intended to be used except through the android.database.sqlite Java classes. If you are accessing this library directly, you are actually breaking the rules.

Beginning with Android N, these rules are going to be enforced.

If your app is using the system SQLite library without using the Java wrapper, it will not be compatible with Android N.

[http://ericsink.com/entries/sqlite_android_n.html](http://ericsink.com/entries/sqlite_android_n.html)

origin - http://www.pipiscrew.com/?p=5845 sqlite-and-android-n