---
title: remove -DSP Manager-
author: PipisCrew
date: 2015-01-16
categories: []
toc: true
---

DSP Manager is the equalizer application for Android, nothing more, is most cases when have sound problems, or you get high CPU process occurred by this application.

how to uninstall (only for rooted devices) :

**solution 1 - using ADB**

> # mount -o remount,rw /system
> # cd /system/app
> # mv DSPManager.apk DSPManager.nouse

**solution 2 - using Root Explorer**

> navigate at /system/app
> find DSPManager.apk rename it to DSPManager.nouse

dont forget to **reboot**

origin - http://www.pipiscrew.com/?p=2201 android-remove-dsp-manager