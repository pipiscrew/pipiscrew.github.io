---
title: IETF approves new internet standards to secure authentication tokens
author: PipisCrew
date: 2018-10-12
categories: [news]
toc: true
---

The Internet Engineering Task Force (IETF) --the organization that develops and promotes Internet standards-- has approved three new standards this week designed to improve the security of authentication tokens against "replay attacks"

Authentication tokens are used everywhere online these days. When a person logs into his Google or Facebook account, an authentication token is generated and stored in a cookie file inside the user's browser.

When the user accesses the Google or Facebook site, instead of asking the user to enter his/her credentials again, the user's browser gives the website the user's authentication token.

But authentication tokens haven't only been used with browser cookies and websites. They are also used inside the OAuth protocol, the JSON Web Token (JWT) standard, and a slew of public or private libraries implementing token-based authentication, often used with APIs and enterprise software solutions.

Hackers have figured out a long time ago that they could steal these tokens instead of users' passwords and access accounts without the need to know a password. Such attacks are known as "replay attacks".

This week, with contributions from Google, Microsoft, and Kings Mountain Systems engineers, the IETF has formally approved three new standards meant to protect token-based authentication systems:

RFC 4871 - The Token Binding Protocol Version 1.0
RFC 4872 - Transport Layer Security (TLS) Extension for Token Binding Protocol Negotiation
RFC 4873 - Token Binding over HTTP

These three standards are meant to add an extra layer of security for the process of generating and negotiating a new access/authentication token.

https://www.zdnet.com/article/ietf-approves-new-internet-standards-to-secure-authentication-tokens/

origin - https://www.pipiscrew.com/2018/10/ietf-approves-new-internet-standards-to-secure-authentication-tokens/ ietf-approves-new-internet-standards-to-secure-authentication-tokens