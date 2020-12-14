---
title: android studio - quick tips
author: PipisCrew
date: 2016-04-09
categories: [android]
toc: true
---

## Add local .aar to project

source - [https://androidbycode.wordpress.com/2015/02/23/building-an-aar-library-in-android-studio/](https://androidbycode.wordpress.com/2015/02/23/building-an-aar-library-in-android-studio/)
source old - [https://teratail.com/questions/25190](https://teratail.com/questions/25190)
You have a few choices as to how to include your AAR library in your project:

-Publish to a external Maven repository
-Publish to a local repository
-Access from a local folder

To include your AAR library as a dependency from a **local folder**:

1. Copy the AAR file into the **libs folder** (aka MyApplication100\app\libs) in your project. Create this folder if it doesn’t exist. It needs to be located in the same folder as your application Gradle build file, not the top level project folder.

2. Declare the libs folder as a dependency repository in your application Gradle script (build.grandle module:app). 

![snap073](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap073.png)

add:
```js
repositories {
    flatDir {
        dirs 'libs'
    }
}
```

3.Declare your AAR library as a dependency:
```js
dependencies {
    compile(name:'facebook-android-sdk-4.10.0', ext:'aar')
}
```

![snap075](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap075.png)

nah, facebook is monster I got an error that cant find a facebook package resources
Error:(22) No resource identifier found for attribute 'cardBackgroundColor' in package 'package_name'
Error:(22) No resource identifier found for attribute 'cardElevation' in package 'package_name'

oops!? ok lets try the newbie way (Add from repository)

![snap081](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap081.png)

then 
Build > Make PRJ 
Build > Make module app

done! compiled! success! 

* * *

## Where is the debug keystore (wtf?)

If **ANDROID_SDK_HOME** defined, then file placed in SDK's subfolder named .android .
When not defined is at the same location as eclipse : %HOMEPATH%\.android\debug.keystore
source - [http://stackoverflow.com/a/30908688/1320686](http://stackoverflow.com/a/30908688/1320686)

## Set the release keystore file

Goto File > PRJ settings > Signing
![snap076](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap076.png)

* * *

## Auto Import

Go to File -> Settings -> Editor -> General >  Auto Import ->

Select Insert imports on paste value to **All**

check Add unambigious imports on the fly 
check Optimize imports on the fly

![snap077](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap077.png)

* * *

## Delete a module

![snap082](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap082.png)

* * *

## Can't add any items to activity_main.xml in Android Studio

source - http://stackoverflow.com/a/33132551
According to new design method followed in android studio for android development you cannot add any elements to the **activity_main.xml**. Rather you should add them to **content_main.xml**.

* * *

## Reset to default configuration in android studio

source - [http://stackoverflow.com/a/19397632/1320686](http://stackoverflow.com/a/19397632/1320686)

Go to your User Folder - on Windows 7/8 this would be:

[SYSDRIVE]:\Users\[your username] (ex. C:\Users\JohnDoe\)

In this folder there should be a folder called .AndroidStudioBeta or .AndroidStudio (notice the period at the start - so on some OSes it would be hidden).

* * *

## Unable to obtain debug bridge (can't locate ADB) 

File > Settings > App&Behavior > System Settings > Android SDK > SDK tools *TAB* > check Android SDK Platform-Tools (mark it & apply)

* * *

## Install support library 

File > Settings > App&Behavior > System Settings > Android SDK > SDK tools *TAB* > check Android Support Library (mark it & apply)

find installed [http://stackoverflow.com/a/20754819/1320686](http://stackoverflow.com/a/20754819/1320686)

* * *

## Set build version

Go to > File > Project Structure > Build Tools (select one from combo, the values comes from androidSDK installed versions)

* * *

## Could not find any version that matches com.android.support:appcompat-v7:15.+

on PRJ build.gradle (Module : app) replace the com.android.support:appcompat-v7:15.+ with com.android.support:appcompat-v7:18.0.+

* * *

## Could not find any version that matches com.android.support:support-v4:15.+

on PRJ build.gradle (Module : app) replace the com.android.support:support-v4:15.+ with com.android.support:support-v4:19.+

* * *

## libs directory in Android Studio

libs dir exists by default (when project created), when user is at #Android# section doesnt see it. Switch to #Project# section or browse at application folder, you will find it at app\libs.

then on PRJ build.gradle (Module : app) add to dependencies tag  : 
```js
compile files('libs/your_jar_name.jar')
```

*OR* turn to #Project# go to app>libs>rclick the jar choose 'Add as Library'

warning - Avoid Referencing Local JARs in Android and Java Libraries - [http://www.alonsoruibal.com/my-gradle-tips-and-tricks/](http://www.alonsoruibal.com/my-gradle-tips-and-tricks/)

*OR*
[http://stackoverflow.com/a/32087456/1320686](http://stackoverflow.com/a/32087456/1320686)

* * *

## This Activity already has an action bar supplied by the window decor. Do not request Window.FEATURE_SUPPORT_ACTION_BAR and set windowActionBar to false in your theme to use a Toolbar instead.

AndroidManifest.xml:

```js
//http://stackoverflow.com/a/34461978/1320686
<activity android:name=".activity.YourActivity" android:theme="@style/AppTheme.NoActionBar">
```

* * *

## I created a android studio default project with drawer but when expand covers toolbar

merge all as : 
```js
//author - Yazhini
//activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.coordinatorlayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:app="http://schemas.android.com/apk/res-auto" xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent" android:layout_height="match_parent" android:fitssystemwindows="true">

    <android.support.design.widget.appbarlayout android:layout_width="match_parent" android:layout_height="wrap_content" android:theme="@style/AppTheme.AppBarOverlay">

        <android.support.v7.widget.toolbar android:id="@+id/toolbar" android:layout_width="match_parent" android:layout_height="?attr/actionBarSize" android:background="?attr/colorPrimary"></android.support.v7.widget.toolbar>

    </android.support.design.widget.appbarlayout>

    <android.support.v4.widget.drawerlayout android:id="@+id/drawer_layout" android:layout_width="match_parent" android:layout_height="match_parent" app:layout_behavior="@string/appbar_scrolling_view_behavior">

        <android.support.design.widget.navigationview android:id="@+id/nav_view" android:layout_width="wrap_content" android:layout_height="match_parent" android:layout_gravity="start" android:fitssystemwindows="true" app:headerlayout="@layout/nav_header_main" app:menu="@menu/activity_main_drawer"></android.support.design.widget.navigationview>

    </android.support.v4.widget.drawerlayout>

    <include layout="@layout/content_main"></include>

    <android.support.design.widget.floatingactionbutton android:id="@+id/fab" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_gravity="bottom|end" android:layout_margin="@dimen/fab_margin" android:src="@android:drawable/ic_dialog_email"></android.support.design.widget.floatingactionbutton>

</android.support.design.widget.coordinatorlayout>
```</activity>

origin - http://www.pipiscrew.com/?p=3817 android-studio-quick-tips