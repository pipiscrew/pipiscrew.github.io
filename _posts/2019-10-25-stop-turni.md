---
title: Stop turning off CURLOPT_SSL_VERIFYPEER and fix your PHP config
author: PipisCrew
date: 2019-10-25
categories: [php]
toc: true
---

There’s a whole lot of misinformation about how to deal with the error “SSL certificate problem, verify that the CA cert is OK” from curl. Nearly everyone advises that you turn CURLOPT_SSL_VERIFYPEER off. This is bad, because it allows your nice, encrypted stream of confidential data to be silently highjacked by a bad guy. Don’t do that! Instead, just fix your PHP installation so that it doesn’t get that error.

The error is caused by not having an up-to-date bundle of **CA root certificates**. This is typically a text file with a bunch of cryptographic signatures that curl uses to verify a host’s SSL certificate. You need to make sure that your installation of PHP has one of these files, and that it’s up to date.

You need to download the CA root certificate bundle and tell PHP where to find it. The [curl website has the latest CA root certificate bundle](https://curl.haxx.se/docs/caextract.html) ready to go, just download the .pem and save it where your PHP installation can access it.

Then you just need to edit your php.ini file to tell curl where you saved the .pem file. On my Windows test VM, I have several PHP versions under c:\php, so I put the file into that folder and added this line to each **php.ini** file:

```jscurl.cainfo=c:\php\cacert.pem```

After restarting the web service, curl now has a valid CA root certificate bundle and it can verify the SSL certificates of remote servers just fine. If it does get an error, it’s because the certificate is invalid.

if for any reason you dont have access to **php.ini**, on curl call specific the CA certificates with :
```js //src -- https://curl.haxx.se/libcurl/c/CURLOPT_CAINFO.htm
curl_setopt($ch, CURLOPT_CAINFO, "cabundle.pem");```

src - https://snippets.webaware.com.au/howto/stop-turning-off-curlopt_ssl_verifypeer-and-fix-your-php-config/
ref - https://phpsecurity.readthedocs.org/en/latest/_articles/PHP-Security-Default-Vulnerabilities-Security-Omissions-And-Framing-Programmers.html
ref - [CURLOPT_SSLCERT](https://curl.haxx.se/libcurl/c/CURLOPT_SSLCERT.html)

origin - https://www.pipiscrew.com/?p=15591 stop-turning-off-curlopt_ssl_verifypeer-and-fix-your-php-config