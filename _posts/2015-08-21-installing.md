---
title: Installing Node and npm
author: PipisCrew
date: 2015-08-21
categories: [js,news]
toc: true
---

reference
[http://blog.modulus.io/build-your-first-http-server-in-nodejs](http://blog.modulus.io/build-your-first-http-server-in-nodejs)

ask for help 
https://webchat.freenode.net/
at channels : #node.js or #npm

0-you need SSH access

1-
http://nvm.sh, run the `curl` command in the readme

2-
then do 
nvm install node && nvm alias default node

3-then read file with
cat ~/.bashrc

you must see two line mention nvm

3-restart terminal application

4-now on root you should have .nvm, type nvm --version 
writes the version

5-execute 
nvm install node && nvm alias default node

6-node installed
	@ ~/ create a dir near public_html name it testnode then create a file into with command (or upload a index.js) :

	echo data > index.js

	go to url FTP software and edit it.. :
```js
//Lets require/import the HTTP module
var http = require('http');

//Lets define a port we want to listen to
const PORT=8080; 

//We need a function which handles requests and send response
function handleRequest(request, response){
	response.end('It Works!! Path Hit: ' + request.url);
}

//Create a server
var server = http.createServer(handleRequest);

//Lets start our server
server.listen(PORT, function(){
	//Callback triggered when server is successfully listening. Hurray!
	console.log("Server listening on: http://localhost:%s", PORT);
});

```

executing
~/testnode>node index.js 
listens on :8080

:)
<ht>

**to uninstall** 
rm -rf testnode
rm -rf .nvm

remove the 2lines from ~/.bashrc

* * *

reference
Installing/Building Node.js - [https://github.com/joyent/node/wiki/Installation](https://github.com/joyent/node/wiki/Installation)
PuTTY - [http://www.chiark.greenend.org.uk/](http://www.chiark.greenend.org.uk/)
The Road to Node – Setting Up node.js on Bluehost - [http://jonat.hn/wp/the-road-to-node-setting-up-node-js-on-bluehost/](http://jonat.hn/wp/the-road-to-node-setting-up-node-js-on-bluehost/)
Installing Node.js on Hostmonster / Bluehost Accounts - http://rcrisman.net/article/10/installing-nodejs-on-hostmonster-bluehost-accounts

Use one of these techniques to install node and npm without having to sudo

[https://gist.github.com/isaacs/579814](https://gist.github.com/isaacs/579814)
or
[https://www.joyent.com/blog/installing-node-and-npm/](https://www.joyent.com/blog/installing-node-and-npm/)

similar - [https://github.com/creationix/nvm/](https://github.com/creationix/nvm/)

![snap193](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap193.png)

![snap194](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap194.png)</ht>

origin - http://www.pipiscrew.com/?p=1581 installing-node-and-npm