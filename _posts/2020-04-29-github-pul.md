---
title: Github Pull / Push Error - RPC failed
author: PipisCrew
date: 2020-04-29
categories: [news]
toc: true
---

> RPC failed; HTTP 500 curl 22 The requested URL returned error The remote end hung up unexpectedly

**nginx**
```js
at nginx.conf in http block add 
client_max_body_size 50m;
```

**apache**
```js
at httpd.conf in <directory></directory> block add
LimitRequestBody 52428800
```

**Internet Information Services (IIS) Manager**
```js
-Expand the Server field
-Expand Sites
-Select the site you want to make the modification for.
-In the Features section, double click Configuration Editor
-Under Section select: system.webServer > serverRuntime
-Modify the uploadReadAheadSize section (The value must be between 0 and 2147483647.)
-Click Apply
-Restart the Website
```

src - https://stackoverflow.com/questions/7489813/github-push-error-rpc-failed-result-22-http-code-413/

ref - https://confluence.atlassian.com/bitbucketserverkb/git-clone-fails-fatal-the-remote-end-hung-up-unexpectedly-fatal-early-eof-fatal-index-pack-failed-779171803.html

* * *

to dive in error, at command line execute
```js
set GIT_TRACE_PACKET=1
set GIT_TRACE=1
set GIT_CURL_VERBOSE=1

// > out.txt 2> error.txt -- redirect output to files, open the error.txt

git clone <remote-repo> > out.txt 2> error.txt
or
git clone --single-branch --branch   
 <remote-repo> > out.txt 2> error.txt

```</remote-repo></remote-repo>

origin - https://www.pipiscrew.com/?p=18356 github-pull-push-error-rpc-failed