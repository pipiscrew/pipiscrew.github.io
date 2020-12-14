---
title: Unlocking an Access VBA Project
author: PipisCrew
date: 2020-11-09
categories: [news]
toc: true
---

Open the database file in any HEX Editor of your choosing.

Find any and all occurrences of the term DPB= and change the B to another value.

Open the newly saved file in Access (like you would normally) and then go into the VBA editor.  You will receive several error messages, simply dismiss them all (and yes, there can be quite a few!).

Open the Database Properties which will now have no password specified.

Enter a new password and confirm it to resecure the VBA Project with a known password.

Save the VBA Project

Close the database

src - https://www.devhut.net/2018/05/03/access-unlocking-an-access-vba-project/
ref - http://www.mendipdatasystems.co.uk/access-security-by-version/4594444347

#mdb

origin - https://www.pipiscrew.com/?p=19350 unlocking-an-access-vba-project