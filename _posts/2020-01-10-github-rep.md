---
title: GitHub Repository Manipulation
author: PipisCrew
date: 2020-01-10
categories: [app,news]
toc: true
---

Github - Adding a files/folders to a repository using git cmd
[http://docdroid.net/cTiXuHE](http://docdroid.net/cTiXuHE)

Github - Creating Releases
[http://docdroid.net/6WP4LYo](http://docdroid.net/6WP4LYo)

Github - Cloning a repository
[http://docdroid.net/yRhvXe0](http://docdroid.net/yRhvXe0)

Github - Deleting a repository
[http://docdroid.net/PZx9UWq](http://docdroid.net/PZx9UWq)

Git download :
[https://git-scm.com/download/win](https://git-scm.com/download/win)

1-extract/install edition
2-put the following dirs to #PATH Environment# (https://www.pipiscrew.com/2017/02/gui-editor-for-windows-environment-variables/)
C:\Program Files (x86)\Git\ (this needed for git-bash.exe)
C:\Program Files (x86)\Git\cmd
C:\Program Files (x86)\Git\bin
3-use the github documents to make any activity

```js
-create repository at github
-git clone https://github.com/x/x.git
-goto to the new 'local dir repository', copy any folder/file you want
-go to root 'local dir repository' exec :

//avoid "LF will be replaced by CRLF"
git config core.autocrlf true 
git add .
git commit -m "first commit"
git push -u origin master

```

[Numerous undo possibilities in Git](https://docs.gitlab.com/ee/topics/git/numerous_undo_possibilities_in_git/)

use chrome octotree v2.4.4 plugin - https://github.com/buunguyen/octotree

use markdown editor - https://stackedit.io/editor

use web2pdf - http://webpagetopdf.com/

Git Essentials Crash Course - https://www.jee.gr/git-essentials-crash-course/

origin - http://www.pipiscrew.com/?p=6680 github-repository-manipulation