---
title: Making -npm install- Safe
author: PipisCrew
date: 2019-07-30
categories: [js]
toc: true
---

NPM have some great stats, they say that there are over 1.3 billion downloads of NPM packages on an average Tuesday.

NPM has this great quote, they say that 97% of the code and a modern web application comes from NPM, and an individual developer is responsible only for the final 3% that makes their application useful and unique.  

Here are some more stats from NPM, there are over 800,000 packages in NPM, making it the largest open source code repository in the world. The average modern web application has over 1,000 dependencies. If we look at something like a create-react-app, which is supposedly bundling together all of the dependencies that you need as a beginning react developer, that has over 1,700 dependencies, so there's a lot of code reuse going on here.

NPM has this great quote, they say that 97% of the code and a modern web application comes from NPM, and an individual developer is responsible only for the final 3% that makes their application useful and unique.

This actually is a pattern of attacks. You might have heard of the event stream incident that happened last November. What happened there was that there was an open source JavaScript developer, Dominic Tarr, who had over a hundred open source packages that he was maintaining. A volunteer came up to him and said, "You know what? I would really like to take over the event stream package. I'll take that off your hands." Dominic Tarr said, "Great. That sounds great." This volunteer made some changes and he actually added a malicious dependency, and that malicious dependency to the venturing and package targeted a specific cryptocurrency wallet. What it did was that it tried take the bitcoin private keys, send it over the network, exfiltrate them and ultimately steal bitcoin.

We saw this pattern again just this month. The electron native notified package also had a malicious dependency that tried to target cryptocurrency wallets. It added a malicious package as a dependency and it required access to the file system and the network. NPM was able to stop this attack, luckily, but I'm sure there are many attacks like this that we're going to see in the future, that if we don't do something to prevent it, we're going to see this pattern again and again.

https://www.infoq.com/presentations/npm-security-realms-ses

origin - https://www.pipiscrew.com/2019/07/making-npm-install-safe/ making-npm-install-safe