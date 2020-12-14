---
title: integrate admob
author: PipisCrew
date: 2014-08-10
categories: []
toc: true
---

references :
<span style="font-family: Consolas, Monaco, monospace; font-size: 12px; line-height: 18px;">[http://apps.admob.com](http://apps.admob.com)
</span><span style="font-family: Consolas, Monaco, monospace; font-size: 12px; line-height: 18px;">[https://developers.google.com/mobile-ads-sdk/docs/
](https://developers.google.com/mobile-ads-sdk/docs/)[https://developers.google.com/mobile-ads-sdk/docs/admob/fundamentals#play](https://developers.google.com/mobile-ads-sdk/docs/admob/fundamentals#play)</span>

*1*
From SDK Manager.exe download the 'Google Play Services' by Extras
![](https://www.pipiscrew.com/wp-content/uploads/2014/08/snap870.png "snap870")
*2*
will download the library + samples
C:\androidSDK\extras\google\google_play_services

import google_play_services to eclipse! (be sure that **copy to workspace** is checked)
![](https://www.pipiscrew.com/wp-content/uploads/2014/08/snap873.png "snap873")

![](https://www.pipiscrew.com/wp-content/uploads/2014/08/snap875.png "snap875")

*3*
Make the reference
![](https://www.pipiscrew.com/wp-content/uploads/2014/08/snap872.png "snap872")

*4*
add to application tag the :

```js
    </meta-data>

    <activity android:name="com.google.android.gms.ads.AdActivity" android:configchanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"></activity>
```

make sure you add the needed permissions :

```js
  <uses-permission android:name="android.permission.INTERNET"></uses-permission>
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
```

*5*
At the activity you like to appear the ad, on XML should be a linearlayout :

```js
    <linearlayout android:id="@+id/linearLayoutAD" android:layout_width="match_parent" android:layout_height="wrap_content" android:orientation="vertical">
    </linearlayout>
```

public variables :

```js
  /** The view to show the ad. */
  private AdView adView;

  /* Your ad unit id. Replace with your actual ad unit id. */
  private static final String AD_UNIT_ID = "INSERT_YOUR_AD_UNIT_ID_HERE";
```

onCreate add :

```js
		///////////
		// Create an ad.
		adView = new AdView(this);
		adView.setAdSize(AdSize.BANNER);
		adView.setAdUnitId(AD_UNIT_ID);

		// Add the AdView to the view hierarchy. The view will have no size
		// until the ad is loaded.
		LinearLayout layout = (LinearLayout) findViewById(R.id.linearLayoutAD);
		layout.addView(adView);

		// Create an ad request. Check logcat output for the hashed device ID to
		// get test ads on a physical device.
		AdRequest adRequest = new AdRequest.Builder()
		.addTestDevice(AdRequest.DEVICE_ID_EMULATOR)
		.addTestDevice("INSERT_YOUR_HASHED_DEVICE_ID_HERE")
		.build();

		// Start loading the ad in the background.
		adView.loadAd(adRequest);
		/////////
```

at logcat you will get :
<span style="color: #ff0000;">The Google Play services resources were not found. Check your project configuration to ensure that the resources are included.</span>

[https://developers.google.com/mobile-ads-sdk/kb/#resourcesnotfound](https://developers.google.com/mobile-ads-sdk/kb/#resourcesnotfound)

origin - http://www.pipiscrew.com/?p=1177 android-integrate-admob