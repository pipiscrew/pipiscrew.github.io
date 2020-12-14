---
title: Last Brave version without Bat service
author: PipisCrew
date: 2020-07-31
categories: [app]
toc: true
---

**Brendan Eich** created **JavaScript** while he was working **at Netscape**. After Internet Explorer killed Netscape, he **co-founded Mozilla** and restarted the browser wars to take down Internet Explorer with Firefox. Several years later, when Google dominated the web with Chrome, Eich **created Brave** to fundamentally change the economics of the internet.

src
https://hackernoon.com/how-google-collapsed-b6ffa82198ee
https://thenewstack.io/brendan-eich-on-creating-javascript-in-10-days-and-what-hed-do-differently-today/?ref=hackernoon.com

--

**v0.59.35**
<div style="padding-left: 30px;">
[https://github.com/brave/brave-browser/releases/tag/v0.60.45](https://github.com/brave/brave-browser/releases/tag/v0.60.45)
started the **Bat Ledger Service**
in detail :
![](https://i.imgur.com/cNBEo7j.png)

use the last **Bat free** w/ Chromium 72.0.3626.81 - [https://github.com/brave/brave-browser/releases/tag/v0.59.35](https://github.com/brave/brave-browser/releases/tag/v0.59.35)

add these to [hosts](https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/) file :

```js
127.0.0.1 go-updater.brave.com
127.0.0.1 laptop-updates.brave.com
```

* * *

add these files to block the ad domains in brave profile, instructions included (these coming from v0.57, before Bat rewards)

```js
by default - %localappdata%\BraveSoftware\Brave-Browser\User Data\afalakplffnnnlkncjhbmahjfjhmlkal

https://www.mediafire.com/file/u4zi83uo2347wue/brave_block_list_by_brave.zip/file
```
</div>

* * *

## Use version with bat service and block unwanted

**v1.4.96 w/ Chromium v80.0.3987.132**
<div style="padding-left: 30px;">
https://github.com/brave/brave-browser/releases/tag/v1.4.96

-hosts file must be blank
-download&install BraveBrowserStandaloneSetup.exe
-goto installation folder and delete 80.1.4.96\Installation folder
-fireup the application, do your preferences, 

![alt](https://i.imgur.com/QjwIoL8.png)

browse for 5 min, this will give you the needed **brave global addons** where exist to 

```js
%localappdata%\BraveSoftware\Brave-Browser\User Data\

afalakplffnnnlkncjhbmahjfjhmlkal - Brave Local Data Files Updater extension (v1.0.22 - 86.2kb)
cffkpbalmllkdoenhmdmpbkajipdjfam - Brave Ad Block Updater extension (v1.0.511 - 5.12mb)
nckpknljimkeefilndhgljafclhkjcfj - Brave NTP sponsored images component (v1.0.25 - null)
oofiananboodjbbmdelgdommihjbkfag - Brave HTTPS Everywhere Updater extension (v1.0.14 - 3.68mb)
```

-close the browser

-add these to [hosts file](https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/) :
```js
// src - https://github.com/brave/brave-browser/blob/a64bfee474d2052934850e189a2166fc8a991df2/lib/whitelistedUrlPrefixes.js

127.0.0.1 go-updater.brave.com
127.0.0.1 laptop-updates.brave.com
127.0.0.1 updates.bravesoftware.com
127.0.0.1 p3a.brave.com
127.0.0.1 tor.bravesoftware.com
127.0.0.1 redirector.brave.com
127.0.0.1 safebrowsing.brave.com
127.0.0.1 brave-core-ext.s3.brave.com
127.0.0.1 static.brave.com
127.0.0.1 static1.brave.com
127.0.0.1 componentupdater.brave.com
127.0.0.1 crlsets.brave.com
127.0.0.1 ledger.mercury.basicattentiontoken.org
127.0.0.1 ledger-staging.mercury.basicattentiontoken.org
127.0.0.1 balance.mercury.basicattentiontoken.org
127.0.0.1 balance-staging.mercury.basicattentiontoken.org
127.0.0.1 publishers.basicattentiontoken.org
127.0.0.1 publishers-staging.basicattentiontoken.org
127.0.0.1 updates.bravesoftware.com
127.0.0.1 publishers-distro.basicattentiontoken.org
127.0.0.1 publishers-staging-distro.basicattentiontoken.org
```

you will end up with :
![alt](https://i.imgur.com/gY3m5YJ.jpg)

</div>

* * *

24/03/2020 - [Brave partners with Binance to let you trade crypto assets from your browser](https://techcrunch.com/2020/03/24/brave-partners-with-binance-to-let-you-trade-crypto-assets-from-your-browser/)

20/03/2020 - [Brave is promoting etoro affiliate program and making a fortune from its users who will likely lose their money](https://github.com/brave/brave-browser/issues/8793)

07/03/2020 - [The Brave Browser is Brilliant](https://rudism.com/the-brave-browser-is-brilliant/)

#brave

origin - https://www.pipiscrew.com/?p=17469 last-brave-version-without-bat-service