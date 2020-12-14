---
title: holo themes with backward compatibility
author: PipisCrew
date: 2014-08-10
categories: []
toc: true
---

references
[ http://www.chilisapps.com/blog/2012/04/17/support-holo-and-older-themes-in-android/](http://www.chilisapps.com/blog/2012/04/17/support-holo-and-older-themes-in-android/)
[ http://stackoverflow.com/questions/9681648/how-to-use-holo-light-theme-and-fall-back-to-light-on-pre-honeycomb-devices](http://stackoverflow.com/questions/9681648/how-to-use-holo-light-theme-and-fall-back-to-light-on-pre-honeycomb-devices)
[http://developer.android.com/about/dashboards/index.html](http://developer.android.com/about/dashboards/index.html)

Many times we would like to support SDK 2.x till 9.x 
```js
    <uses-sdk android:minsdkversion="8" android:targetsdkversion="16"></uses-sdk>
```

what about when SDK >= 3 use the holo theme and when < 3="" use="" the="" black="" one?="" alright,="" lets="" create="" custom="" themes!="" thanks="" **aracem**="" **values/themes.xml="" -=""><span style="color: #ff0000;">(Android 2.0+)</span>**
```js
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="MyAppTheme" parent="@android:style/Theme.Light.NoTitleBar">
        <!-- Any customizations for your app running on pre-3.0 devices here -->
    </style>
</resources> 
```

**values-v11/themes.xml - <span style="color: #ff0000;">(Android 3.0+)</span>**
```js
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="MyAppTheme" parent="@android:style/Theme.Holo.Light">

    </style>
</resources>
```

**values-v14/themes.xml - <span style="color: #ff0000;">(Android 4.0+)</span>**
```js
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="MyAppTheme" parent="@android:style/Theme.DeviceDefault.Light.NoActionBar">

    </style>
</resources>
```

manifest
```js
 <application ...="" android:theme="@style/MyAppTheme">
```</application>

origin - http://www.pipiscrew.com/?p=1187 android-holo-themes-with-backward-compatibility