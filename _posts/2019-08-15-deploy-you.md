---
title: Deploy your angular2 app to Heroku
author: PipisCrew
date: 2019-08-15
categories: [js,php,angular]
toc: true
---

1-Create an account to https://heroku.com (similar https://c9.io)
2-Download the Heroku CLI (git required)
https://cli-assets.heroku.com/branches/stable/heroku-windows-386.exe
or x64 https://cli-assets.heroku.com/branches/stable/heroku-windows-amd64.exe
or https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up
2b-To login to your account must use 
```js
//https://stackoverflow.com/a/44879715/1320686
heroku login

and not plain heroku
```
3-Create a new folder C:\PRJ
4-Copy your project to C:\PRJ **without** the **node_modules** directory, as result to have the C:\PRJ\package.json. 

Modifications :
the key ***devDependencies*** doesnt take place @ heroku, delete it!
One quick solution is to copy all ***devDependencies*** children to ***dependencies*** key (angular/*cli required for build). Will work.

* * *

This is the package.json minimal&working for angular2 v4.0 :

lines removed **test+lint+ee**

The line 7 replaced 
The **start** tells to heroku what to do on host instantiation.

The line 9 added, didnt exist to package.json.
The **postinstall** tells what to do when the heroku build called (aka calling to build the release via **ng**)

The lines 26,27 added, didnt exist to package.json.
The **express** tells to install node express (https://expressjs.com/), to serve the files.
The **serve-favicon** install the node package, so browser display the page icon to tab!
```js
{
  "name": "mapp",
  "version": "0.0.0",
  "license": "MIT",
  "scripts": {
    "ng": "ng",
    "start": "node server.js",
    "build": "ng build",
    "postinstall": "ng build --aot -prod"
  },
  "private": true,
  "dependencies": {
    "@angular/common": "^4.0.0",
    "@angular/compiler": "^4.0.0",
    "@angular/core": "^4.0.0",
    "@angular/forms": "^4.0.0",
    "@angular/http": "^4.0.0",
    "@angular/platform-browser": "^4.0.0",
    "@angular/platform-browser-dynamic": "^4.0.0",
    "@angular/router": "^4.0.0",
    "@angular/cli": "1.0.0",
    "@angular/compiler-cli": "^4.0.0",
    "core-js": "^2.4.1",
    "rxjs": "^5.1.0",
    "zone.js": "^0.8.4",
    "express": "~4.9.8",
    "serve-favicon": "~2.3.0"
  }
}
```

5-create a new file C:\PRJ\server.js for node **express** configuration as 
```js
// server.js
const express = require('express');
const path = require('path');
const favicon = require('serve-favicon');
const app = express();

// If an incoming request uses
// a protocol other than HTTPS,
// redirect that request to the
// same url but with HTTPS
const forceSSL = function() {
  return function(req, res, next) {
    if (req.headers['x-forwarded-proto'] !== 'https') {
      return res.redirect(
        ['https://', req.get('Host'), req.url].join('')
      );
    }
    next();
  }
};

// Instruct the app
// to use the forceSSL
// middleware
//app.use(forceSSL());

// For all GET requests, send back index.html
// so that PathLocationStrategy can be used
/*
app.get('/*', function(req, res) {
  res.sendFile(path.join(__dirname + '/dist/index.html'));
});
*/

// Run the app by serving the static files
// in the dist directory
app.use(express.static(__dirname + '/dist'));
// Start the app by listening on the default
// Heroku port
app.listen(process.env.PORT || 4200, function() {
  console.log('Listening on port ' + this.address().port); //Listening on port 8888
});
``` 

6-we are on C:\PRJ contains all the needed files for deploy, go with 
```js
git init
git config core.autocrlf true
git add .
git commit -m "first commit"
heroku create
git push heroku master
heroku open
```

before push the files, you can test it locally with : 
```js
npm install //reads the package.json
node server.js // runs the server
```

once you test dont forget to delete the **node_modules** directory, before the deploy.

* * *

of course you can skip all the angular part and install an apache, build local the angular release and deploy it ;). But all made for shake of exercise. Lets see the easy way!

The best way to use heroku for angular, is to submit an index.php file. Heroku installs automatically apache.
Afterwards you can create folders to your local repository, like 
	angularapp1
	angularapp2

compile the angular applications locally and submit it to remote repository. Will be available at https://x.herokuapp.com/angularapp1 

Warning because the angular app running inside the directory and not on root of url, you have to compile it with the **base-href** parameter
```jsng build --prod --aot --base-href ./```

```js
1-create C:\PRJ
2-create a file index.php paste&save
	<?php echo="" "this="" is="" a="" test";=""?>
3-create the angularapp1 folder & copy the files from angular #dist# folder
4-Goto C:\PRJ and execute
	git init
	git config core.autocrlf true
	git add .
	git commit -m "first commit"
	heroku create
	git push heroku master
	heroku open

afterwards any modification made to C:\PRJ, you can use the following to upload it to remote repository
	heroku git:clone -a myapp
	git add .
	git commit -m "second commit"
	git push heroku master
```

Another thing with PHP repository is that you can submit a **composer.json** & composer.lock, once the files uploaded Heroku will automatically download the dependencies to your heroku repository :)
for example **mbstring** is not installed by default, Im using 

```js
//composer.json
{
	"require": {
	  "ext-mbstring": "*"
	}
}

//composer.lock
{
    "_readme": [
        "This file locks the dependencies of your project to a known state",
        "Read more about it at https://getcomposer.org/doc/01-basic-usage.md#composer-lock-the-lock-file",
        "This file is @generated automatically"
    ],
    "content-hash": "adc392ef7340a30855efcdacc40133fd",
    "packages": [],
    "packages-dev": [],
    "aliases": [],
    "minimum-stability": "stable",
    "stability-flags": [],
    "prefer-stable": false,
    "prefer-lowest": false,
    "platform": {
        "ext-mbstring": "*"
    },
    "platform-dev": []
}
```

In general navigate at http://php.net/manual/en/extensions.php found the extension you want, the URL ends with **book.bzip2.php** so will be **ext-bzip2**

* * *

install pdo-sqlite via composer.json
```js
//ref - https://devcenter.heroku.com/articles/php-support
//before deploy you have to run once to generate the composer.lock :
//composer update
{
    "require": {
        "ext-pdo_sqlite": "*"
    }
}
```

then you are able to
```js
    $dbh = new PDO('sqlite:x.db', '', '', array(
	 PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
	));

//see error log @ https://dashboard.heroku.com/apps/myapp/logs
```

Added database records are deleted after restarting app - https://stackoverflow.com/q/36454885/1320686
Using Sqlite on Heroku - https://larry-price.com/blog/2014/03/29/using-sqlite-on-heroku

Heroku has ephemeral file system. At each request a new environment is cloned and destroyed. You should store SQL lite files on amazon or use an Heroku database (Postgres / Redis).

Create Heroku database - https://data.heroku.com/

on Postgres free plan (https://devcenter.heroku.com/articles/heroku-postgres-plans#plan-tiers) :
-expected uptime 99.5% (< 4="" hr="" downtime="" per="">  

-rows limit 10,000  

-concurrent connections limit 20  

[Official - How to connect in PHP](https://devcenter.heroku.com/articles/heroku-postgresql#connecting-in-php)
[Github - raw sample by plehr](https://github.com/plehr/Heroku-and-PDO/blob/master/postgree.php)
[Official - Connecting to Heroku Postgres Databases from Outside of Heroku](https://devcenter.heroku.com/articles/connecting-to-heroku-postgres-databases-from-outside-of-heroku)

howto on github - https://github.com/pipiscrew/DBManager/tree/master/2_patterns/heroku

* * *

you can find a ready to use heroku at 
https://www.pipiscrew.com/2017/02/tired-of-nodenpm-and-composer-and-git-installations/

Greets to Ryan Chenkie & codesandtags

ref -
https://medium.com/@ryanchenkie_40935/angular-cli-deployment-host-your-angular-2-app-on-heroku-3f266f13f352
https://github.com/codesandtags/angular2-webpack-heroku
https://scotch.io/tutorials/how-to-deploy-a-node-js-app-to-heroku
https://devcenter.heroku.com/articles/getting-started-with-nodejs#deploy-the-app
https://expressjs.com/en/guide/routing.html

origin - http://www.pipiscrew.com/?p=7475 deploy-your-angular2-app-to-heroku