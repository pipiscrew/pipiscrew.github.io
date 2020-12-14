---
title: android-support-v7-appcompat on PRJ for 4.1 (SDK16)
author: PipisCrew
date: 2016-03-05
categories: [android]
toc: true
---

using android-support-v7-appcompat on a android project with android:minSdkVersion="16"

*1*
The #SDK Tools# and #SDK Platform tools# must be >= 23
![snap145](https://www.pipiscrew.com/wp-content/uploads/2016/03/snap145.png)

you must have the #SDK Platform# >= 19, to build android-support-v7-appcompat PRJ (required by android-support-v7-appcompat > project.properties).

Download > Close SDK Manager > Close Eclipse restart

Restart SDK Manager > Download #Android Support Library# (note that this item is not listed on first place)

*2*
Open Eclipse, you got a warning about old ADT version, needs update.. a conflict occured when going to update. The solution manually uninstall the current ADT as :

![snap147](https://www.pipiscrew.com/wp-content/uploads/2016/03/snap147.png)

Help-->Install New Software-->What is already installed?
Then, Select "Android DDMS, Andoid Devlopment Tools,Android Hierarcy Viewer, Android native Development Tools, Android Traceview, Tracer for OpenGL ES" and click Uninstall.
After all this step, try Add link (https://dl-ssl.google.com/android/eclipse/) and name is ADT Plugin. This link will get the latest ADT Plugin. In this way you reinstall the ADT.

*3*
Eclipse> Project Explorer > RClick > Import at C:\aSDK\extras\android\support\v7\appcompat > RClick th PRJ > Properties > Make sure using the proper #SDK Platform#

![snap149](https://www.pipiscrew.com/wp-content/uploads/2016/03/snap149.png)

so finally (after a Project > Clean > android-support-v7-appcompat PRJ) the PRJ built!

*4*
We going to our PRJ > Properties > Android > We set the same #SDK Platform# and also > Add the reference to android-support-v7-appcompat PRJ

![snap151](https://www.pipiscrew.com/wp-content/uploads/2016/03/snap151.png)

my project previous using libs/support4 now I removed it from libs, because support7 includes by default the support4

![snap153](https://www.pipiscrew.com/wp-content/uploads/2016/03/snap153.png)

**bottomline :**
using only support4 the final apk was : 600kb
using support7 the final apk is : 1.66mb

## DDMS stopped work

right click select reset

**references :**
http://stackoverflow.com/a/30151946/1320686
http://blog.axxg.de/android-support-library-v7-appcompat-eclipse-einbinden/

## Download ADT manual (no tried)

http://stackoverflow.com/a/27882868/1320686 
http://dl.google.com/android/adt/adt-bundle-windows-x86-20140702.zip

## Google Stops Development And Support For ADT In Eclipse

[http://www.techtimes.com/articles/64494/20150630/google-stops-development-and-support-for-adt-in-eclipse.htm](http://www.techtimes.com/articles/64494/20150630/google-stops-development-and-support-for-adt-in-eclipse.htm)

* * *

## The type org.apache.http.Header cannot be resolved. It is indirectly referenced from required .class files

In Eclipse copy org.apache.http.legacy.jar from AndroidSDK/platforms/android-23/optional to libs folder. (http://stackoverflow.com/a/32435116/1320686)

origin - http://www.pipiscrew.com/?p=4216 android-android-support-v7-appcompat-on-prj-for-4-1-sdk16