---
title: facebook API v2.0 to 2.4
author: PipisCrew
date: 2015-08-25
categories: [js]
toc: true
---

reference 
[http://stackoverflow.com/a/31363895](http://stackoverflow.com/a/31363895)

Graph API v2.0 FQL - [https://developers.facebook.com/docs/reference/fql/user/](https://developers.facebook.com/docs/reference/fql/user/)

Graph API - [https://developers.facebook.com/docs/graph-api](https://developers.facebook.com/docs/graph-api)

Graph API Changelog - [https://developers.facebook.com/docs/apps/changelog](https://developers.facebook.com/docs/apps/changelog)

Grpah Explorer - [https://developers.facebook.com/tools/explorer/ ](https://developers.facebook.com/tools/explorer/)

by July 8, 2015 any app / page tab created on Facebook using **v2.4** 

code before (till v2.3) :
```js
FB.api('/me', function(response)
{
  console.log(response);
});

```

![snap278](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap278.png)

when run the same code via v2.4

![snap279](https://www.pipiscrew.com/wp-content/uploads/2015/08/snap279.png)

make v2.4 select the needed fields :
```js
FB.api('/me?fields=id,name,email,gender,timezone ', function(response)
{
  console.log(response);
});
```

origin - http://www.pipiscrew.com/?p=1640 facebook-v2-0-to-2-4