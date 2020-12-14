---
title: Issue Your Own Self-Signed S/MIME Certs with OpenSSL
author: PipisCrew
date: 2018-12-16
categories: [news]
toc: true
---

```js
//src - https://gist.github.com/richieforeman/3166387
openssl genrsa -des3 -out ca.key 4096
openssl req -new -x509 -days 365 -key ca.key -out ca.crt
openssl pkcs12 -export -in ca.crt -inkey ca.key -out ca.p12
```

more [Create Self-Signed S/MIME Certificates](https://www.dalesandro.net/create-self-signed-smime-certificates/) by John Dalesandro - [mirror](https://docdroid.net/4HeohFv)

**refs :**
[https://www.ssl.com/how-to/create-a-pfx-p12-certificate-file-using-openssl/](https://www.ssl.com/how-to/create-a-pfx-p12-certificate-file-using-openssl/)

https://security.stackexchange.com/questions/17583/how-do-i-create-a-valid-email-certificate-for-outlook-s-mime-with-openssl

https://stackoverflow.com/a/20445432

https://www.howtoforge.com/how-to-encrypt-mails-with-ssl-certificates-s-mime

https://gist.github.com/essandess/395446556afea7334826e9df74f85edf

* * *

### How to apply at COMODO for free email certification

-By any browser, apply for the [certification](https://sectigo.com/products/signing-certificates/email-smime-certificate) (write down the password you set), wait to receive the COMODO mail
![](https://i.imgur.com/J22rd4Q.png)

Then using **firefox only**, goto the link provided to your mail 
![](https://i.imgur.com/Rj1JNNA.png)

it will ask for your email and password mailed^
![](https://i.imgur.com/Rgg42ZU.png)

**Automatically** will install the **certificate** to firefox, then goto Options > about:preferences#privacy > View Certificates
![](https://i.imgur.com/YWdgAkK.png)

Find the certificate under **Your Certificates** tab 
[![](https://i.imgur.com/pfbMthu.png)](https://i.imgur.com/pfbMthu.png)

Select the certificate and click **Backup button**, will ask for a **password**, use a **new one**, this will generate a **.p12** file.

The certificate is valid for **365 days**.

![](https://i.imgur.com/vGxN3FM.png)

Now open **Thunderbird**, goto Options > Account Settings > Security
[![](https://i.imgur.com/0x8f6nt.png)](https://i.imgur.com/0x8f6nt.png)

Click **Manage Certificates**, click **Import** button and point the **.p12** file generated from **Firefox**. Then click the **Select**

![](https://i.imgur.com/mnNFs0d.png)

Automatically will **find** the **certificate** and ask you :
![](https://i.imgur.com/7tLqHQQ.png)

If you choose yes, you can also encrypt the message body.
Now when you open a New Message window, you can choose to **Digital Sign** it and **encrypt it** if you like.

![](https://i.imgur.com/mbU5Gui.png)
![](https://i.imgur.com/MWVTzRf.png)

source - [http://techies-world.com/install-comodo-email-certificate-in-thunderbird/](http://techies-world.com/install-comodo-email-certificate-in-thunderbird/)

* * *

if you delete the .p12 you **cant recover it**, doing again the procedure, you getting :
![](https://i.imgur.com/YeXZtyC.png)

**web clients**, shows the certificate as attachment :) (always **smime.p7s**)
![](https://i.imgur.com/gBH7XQl.png)

**Thunderbird** - when you sent a signed email, this **envelope** appears
[![](https://i.imgur.com/BR2GdxW.png)](https://i.imgur.com/BR2GdxW.png)

Outlook
![](https://i.imgur.com/1C6RBRt.png)
![](https://i.imgur.com/ZOhBSfe.png)

gmail 
![](https://i.imgur.com/qk6BwAe.png)
![](https://i.imgur.com/WcHgiMR.png)

gmail mobile
![](https://i.imgur.com/qk6BwAe.png)
![](https://i.imgur.com/WcHgiMR.png)

Thunderbird when the certificate is not proper :
[![](https://i.imgur.com/M6m7EsS.png)](https://i.imgur.com/M6m7EsS.png)

* * *

**

### Creating the certificate with openssl

**
The openssl advise to use the precompiled from the following distributors.  ([proof](https://www.openssl.org/community/binaries.html))
download MinGW compiled from [https://bintray.com/vszakats/generic/openssl](https://bintray.com/vszakats/generic/openssl)

**run :**
```js
openssl genrsa -des3 -out ca.key 4096
```

[caption width="775" align="aligncenter"][![](https://i.imgur.com/StVNXoz.png)](https://i.imgur.com/StVNXoz.png) ca.key will generated[/caption]

**run :**
```js
openssl req -new -config openssl.cnf -x509 -days 9999 -key ca.key -out ca.crt
```

[caption width="1057" align="aligncenter"][![](https://i.imgur.com/DgLTTk4.png)](https://i.imgur.com/DgLTTk4.png) we enter our email address^ this will be used to identify the certificate later on outlook.      ca.crt will generated[/caption]

Double click the **ca.crt** 
![](https://i.imgur.com/Kc8Iqve.png)

**run :**
```js
openssl pkcs12 -export -in ca.crt -inkey ca.key -out ca.p12
```
[caption width="877" align="aligncenter"][![](https://i.imgur.com/u57rBpH.png)](https://i.imgur.com/u57rBpH.png) ca.p12 will generated[/caption]

[caption width="171" align="aligncenter"]![](https://i.imgur.com/W5xhi90.png) right click[/caption]

![](https://i.imgur.com/gzDkIfj.png)

[caption width="933" align="aligncenter"][![](https://i.imgur.com/fD3eFyG.png)](https://i.imgur.com/fD3eFyG.png) [windows + R] > certmgr.msc[/caption]

At **outlook**
File > options > trust center > trust center settings > email security > default setting, settings button > Signing Certificate [choose] > automatically verifies the certificate (we enter before our email address) with the account we have to outlook

![](https://i.imgur.com/8gVrWsM.png)

![](https://i.imgur.com/BWpHBD1.png)

Will be identified as :
![](https://i.imgur.com/S9JsDZx.png)

Now, **two new buttons** appear on the **OPTIONS** tab

![](https://i.imgur.com/UyywKCT.png)

when tried to sign my first mail, got
![](https://i.imgur.com/E78oINK.png)

possible [solution](https://support.microsoft.com/en-gb/help/884738/you-receive-an-error-message-when-you-try-to-send-an-encrypted-e-mail) (not tried!).

## non important refs :

For outlook
https://support.quovadisglobal.com/kb/a416/how-do-i-install-my-digital-certificate-into-outlook-2013-to-encrypt-email-or-digitally-sign-emails.aspx
https://knowledge.digicert.com/solution/SO10781.html

For word :
https://support.office.com/en-us/article/add-or-remove-a-digital-signature-in-office-files-70d26dc9-be10-46f1-8efa-719c8b3f1a2d

[How to sign a file with 3rd party app ](https://www.signfiles.com/p7s-signer/)

https://support.comodo.com/index.php?/comodo/Knowledgebase/Article/View/1001/7/how-to-verify-your-code-signing-certificate-is-installed-windows
Obtaining an S/MIME Certificate to Sign Emails
https://support.postbox-inc.com/hc/en-us/articles/202200540-Obtaining-an-S-MIME-Certificate-to-Sign-Emails
https://www.openssl.org/docs/manmaster/man1/smime.html
https://knowledge.digicert.com/solution/SO10781.html
Encrypt messages by using S/MIME in Outlook Web App
https://support.office.com/en-us/article/encrypt-messages-by-using-s-mime-in-outlook-web-app-2e57e4bd-4cc2-4531-9a39-426e7c873e26
Browser Email Certificates FAQ
https://www.instantssl.com/ssl-certificate-support/server_faq/ssl-email-certificate-faq.html

* * *

**PKCS#12 of .pfx or .p12**

The PKCS#12 or PFX format is a binary format for storing the server certificate, any intermediate certificates, and the private key into a single encryptable file. PFX files are usually found with the extensions .pfx and .p12. PFX files are typically used on Windows machines to import and export certificates and private keys. The Personal Information Exchange format (PFX, also called PKCS #12) supports secure storage of certificates, private keys, and all certificates in a certification path. The PKCS #12 format is the only file format that can be used to export a certificate and its private key.

**.CRT or .CER**

CRT is a file extension for a digital certificate file used with a web browser. CRT files are used to verify a secure website’s authenticity, distributed by certificate authority (CA) companies such as GlobalSign, VeriSign and Thawte. ([src](https://codebazz.wordpress.com/2017/08/27/difference-between-p12-pfx-vs-crt-cer-vs-pem-vs-der/))

#OpenSSL #thunderbird #firefox #certificate #pfx #p12 #crt

origin - https://www.pipiscrew.com/?p=14493 issue-your-own-self-signed-smime-certs-with-openssl