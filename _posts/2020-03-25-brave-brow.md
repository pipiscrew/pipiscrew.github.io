---
title: Brave browser to block web fingerprinting
author: PipisCrew
date: 2020-03-25
categories: [news]
toc: true
---

https://nakedsecurity.sophos.com/2020/03/11/brave-browser-to-block-web-fingerprinting-with-randomisation/

demo - https://fingerprintjs.com/demo

A browser is queried for its agent string, screen color depth, language, installed plugins with supported mime types, timezone offset and other capabilities, such as local storage and session storage. Then these values are passed through a hashing function to produce a fingerprint that gives weak guarantees of uniqueness.

[src](https://github.com/Valve/fingerprintjs2)

* * *

> X-client-data header, which Chrome sends to Google when a Google webpage has been requested, represents a unique identifier that can be used to track people across the web

https://www.theregister.co.uk/2020/03/11/google_personally_identifiable_info/

* * *

## Chrome Phasing out Support for User Agent

The most significant usage for the User-Agent remained within the advertising industry, where companies used it to '**fingerprint**' users, a practice that many privacy advocates found to be problematic - mainly as most users had limited options to disable/mask those details. To combat these two problems, the Chrome team will start phasing out the User-Agent beginning with Chrome 81.

While removing the User-Agent completely was deemed problematic, as many sites still rely on them, Chrome will no longer update the browser version and will only include a unified version of the OS data.

The move is scheduled to be complete by Chrome 85 and is expected to be released in mid-September 2020. Other browser vendors, including Mozilla Firefox, Microsoft Edge, and Apple Safari, have expressed their support of the move. However, it's still unclear when they will phase out the User-Agent themselves.

ref
https://www.infoq.com/news/2020/03/chrome-phasing-user-agent/
https://github.com/WICG/ua-client-hints

origin - https://www.pipiscrew.com/?p=17419 brave-browser-to-block-web-fingerprinting