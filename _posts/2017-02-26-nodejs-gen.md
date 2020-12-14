---
title: o[nodeJS] generate signed random numbers via random.org
author: PipisCrew
date: 2017-02-26
categories: [news]
toc: true
---

<span style="text-decoration: underline;">references :</span>

[https://api.random.org/json-rpc/2/introduction](https://api.random.org/json-rpc/2/introduction)

[https://api.random.org/json-rpc/2/](https://api.random.org/json-rpc/2/)

[https://api.random.org/json-rpc/2/error-codes
](https://api.random.org/json-rpc/2/error-codes)

<span style="text-decoration: underline;">alternative libs ready to use for nodeJS :</span>

[https://npmjs.org/package/node-random](https://npmjs.org/package/node-random) or [https://github.com/mikeal/request](https://github.com/mikeal/request)

[https://github.com/Epictetus/random-proxy](https://github.com/Epictetus/random-proxy)

get beta key at [https://api.random.org/api-keys/beta](https://api.random.org/api-keys/beta)

**1-**

install <span style="color: #ff0000;">**request**</span> library at **nodeJS** via [https://npmjs.org/package/request](https://npmjs.org/package/request)

```jsnpm install request```

**2-**

use this code to generate signed numbers :

```js
var request = require('request');
request({
	method : 'PUT',
	uri : 'https://api.random.org/json-rpc/1/invoke',
	headers : {
		'content-type' : 'application/json-rpc'
	},
	body : JSON.stringify({
		"jsonrpc" : "2.0",
		"method" : "generateSignedIntegers",
		"params" : {
			"apiKey" : "your beta API key",
			"n" : 6,
			"min" : 1,
			"max" : 6,
			"replacement" : true,
			"base" : 10
		},
		"id" : 14215 //without this variable you will never get valid response
		             //A request identifier that allows the client to match responses to request. The service will return this unchanged in its response.
	})
}, function(error, response, body) {
        var info = JSON.parse(body);
	//console.log(response.statusCode, body);
        console.log(info.result.random.data);
})
```

is NOT free, from first run on response you will see

```js"bitsUsed":16,"bitsLeft":249904,"requestsLeft":994```

yes pay them by bits or by requests!

ps you can also without APIkey via ```jshttp://www.random.org/integers/?num=1&min=1&max=6&col=1&base=10&format=plain&rnd=new``` again restrictions applied.

origin - http://www.pipiscrew.com/?p=699 nodejs-generate-signed-random-numbers-via-random-org