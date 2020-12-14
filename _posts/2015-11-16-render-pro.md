---
title: render problem!?
author: PipisCrew
date: 2015-11-16
categories: [asp_classic]
toc: true
---

**ASP Classic** magic!

the plot : 
a form is filled and submitted to 3rd party server, passing through also the SHA1 digest.

the problem :
Server Response : Invalid Digest

the cause :
first, make all form elements visible :
[![snap290](https://www.pipiscrew.com/wp-content/uploads/2015/11/snap290.png)](https://www.pipiscrew.com/wp-content/uploads/2015/11/snap290.png)

for unknown reason the variable **orderAmount** on **Location A** appears with decimal symbol . (dot) where on **Location B** appears with decimal symbol , (comma).

origin - http://www.pipiscrew.com/?p=2422 asp-render-problem