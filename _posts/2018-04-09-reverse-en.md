---
title: Reverse engineering WhatsApp Web
author: PipisCrew
date: 2018-04-09
categories: [news]
toc: true
---

WhatsApp Web encrypts the data using several different algorithms. These include AES 256 ECB, Curve25519 as Diffie-Hellman key agreement scheme, HKDF for generating the extended shared secret and HMAC with SHA256.

Starting the WhatsApp Web session happens by just connecting to one of its websocket servers at wss://w[1-8].web.whatsapp.com/ws

https://github.com/sigalor/whatsapp-web-reveng

ref - https://news.ycombinator.com/item?id=16789644

origin - https://www.pipiscrew.com/2018/04/reverse-engineering-whatsapp-web/ reverse-engineering-whatsapp-web