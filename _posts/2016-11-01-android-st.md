---
title: android studio - sign apk
author: PipisCrew
date: 2016-11-01
categories: [android]
toc: true
---

compare to eclipse, you can use the same keystore for debug and release.

source - http://stackoverflow.com/a/17992232 with pictures.

1) Go to File > Project Structure > select project > go to "signing" tab and select your default or any keystore you want and fill all the details. In case you are not able to fill the details, hit the green '+' button. I've highlighted in the screenshot.

2)Goto Build Types> select your build type and select your "Signing Config". In my case, I've to select "config". Check the highlighted region. 

3)File > Save All

4)Restart IDE

origin - http://www.pipiscrew.com/?p=6242 android-studio-sign-apk