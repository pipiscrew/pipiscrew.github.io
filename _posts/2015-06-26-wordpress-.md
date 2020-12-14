---
title: o[wordpress] reset password
author: PipisCrew
date: 2015-06-26
categories: []
toc: true
---

reference
[http://codex.wordpress.org/Resetting_Your_Password](http://codex.wordpress.org/Resetting_Your_Password)

-[http://www.miraclesalad.com/webtools/md5.php](http://www.miraclesalad.com/webtools/md5.php)
-generate the md5 for a password
-goto dbase > and update the users table via UPDATE users SET user_pass='x' where id=x

origin - http://www.pipiscrew.com/?p=3248 wordpress-reset-password