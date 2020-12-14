---
title: deltaxflux.Fluxion
author: PipisCrew
date: 2016-11-01
categories: [news]
toc: true
---

Is a remake of linset by vk496 with less bugs and more features. It's compatible with the latest release of Kali (Rolling). 

-Scan the networks.
-Capture a handshake (can't be used without a valid handshake, it's necessary to verify the password)
-Use WEB Interface *
-Launch a FakeAP instance to imitate the original access point
-Spawns a MDK3 process, which deauthenticates all users connected to the target network, so they can be lured to connect to the FakeAP and enter the WPA password.
-A fake DNS server is launched in order to capture all DNS requests and redirect them to the host running the script
-A captive portal is launched in order to serve a page, which prompts the user to enter their WPA password
-Each submitted password is verified by the handshake captured earlier
-The attack will automatically terminate, as soon as a correct password is submitted

https://github.com/deltaxflux/fluxion

similar --
https://github.com/sophron/wifiphisher

#wpa2

origin - http://www.pipiscrew.com/?p=6233 deltaxflux-fluxion