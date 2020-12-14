---
title: Installing .NET 4.6.2 offline, needs security certificate
author: PipisCrew
date: 2019-03-20
categories: [.net]
toc: true
---

While trying to install the .NET 4.6.2 framework on an offline laptop, I receive the following error, which ends the setup:

> A certificate chain could not be built to a trusted root authority.

solution, install this update (windows7 x64), tested & working :
https://download.microsoft.com/download/1/4/9/14936FE9-4D16-4019-A093-5E00182609EB/Windows6.1-KB2670838-x64.msu

then download the missing certificate by :
http://www.microsoft.com/pki/certs/MicRooCerAut2011_2011_03_22.crt

right click > install to trusted root

run again the framework 4.6.2 installation!

origin - https://www.pipiscrew.com/?p=14775 installing-net-4-6-2-offline-needs-security-certificate