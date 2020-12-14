---
title: Cryptojacking (2019)
author: PipisCrew
date: 2020-03-18
categories: [news]
toc: true
---

Cryptojacking, the theft of computing power to mine digital currency, has been around at least since 2013 – and has shrunk in use dramatically with the death of **Monero-mining** service **Coinhive**.

Since Coinhive's closure last year, cryptojacking has been almost eliminated, according to a group of researchers from the University of Cincinnati in America, and Lakehead University in Canada, because online ads generate more revenue.

**Coinhive provided JavaScript code** that websites could incorporate to make visitors' computers mine **Monero**, a cryptocurrency that happens to appeal to cybercriminals because it's difficult to trace. **Though Coinhive's code was marketed as a monetization alternative** to advertising, it was quickly abused – a mining script can also be injected into a website by hackers without the site owner's knowledge.

When the service launched in September **2017**, **Monero** could be exchanged for about $100 apiece. By early January, 2018, its price **peaked** at almost $500.

On March 8, **2019**, **Coinhive shutdown** because, the company said, the project was no longer economically viable. The price of Monero then was about $50 and today it's trading at around $35.

The researchers used a cryptojacking detector known as [CMTracker](https://github.com/deluser8/cmtracker) to look for cryptojacking code. They evaluated 2,770 websites, manually and automatically, that had been flagged by CMTracker before the Coinhive shutdown. And 99 per cent of them no longer run cryptojacking code. The remaining 1 per cent still do, using eight distinct mining scripts.

    minero.cc/lib/minero.min.js
    webminepool.com/lib/base.js
    hashing.win/46B8.js
    */perfekt/perfekt.js
    */tkefrep/tkefrep.js
    enaure.co/javas.js
    lasimakiz.xyz/sadig6.js
    uvuvwe.bid/jo/jo/miner_compressed/webmr.js

These scripts were subsequently spotted on **632 websites** in the wild. That's a significant decrease from 2017 when Coinhive code alone could be found on more than **30,000 websites**.

https://www.theregister.co.uk/2020/03/17/cryptojacking_coinhive/

origin - https://www.pipiscrew.com/?p=17546 cryptojacking-2019