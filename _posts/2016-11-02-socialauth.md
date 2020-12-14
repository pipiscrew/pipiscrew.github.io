---
title: socialauth-android
author: PipisCrew
date: 2016-11-02
categories: [android]
toc: true
---

homepage : [http://code.google.com/p/socialauth-android/](http://code.google.com/p/socialauth-android/logo?cct=1378999905)
[https://github.com/3pillarlabs/socialauth-android](https://github.com/3pillarlabs/socialauth-android)

onCreate

```js
		// Add providers
		adapter.addProvider(Provider.FACEBOOK, R.drawable.facebook);
		adapter.addProvider(Provider.TWITTER, R.drawable.twitter);
		adapter.addProvider(Provider.GOOGLE, R.drawable.google);

		try {
			adapter.addConfig(Provider.FACEBOOK, "1", "2", null);
			adapter.addConfig(Provider.TWITTER, "1", "2", null);
			adapter.addConfig(Provider.GOOGLE, "1", "2", null);
		} catch (Exception e) {
			e.printStackTrace();
		}
```

Login

```js
	public void btnFB_Click(View view) {
		adapter.authorize(LoginActivity.this, Provider.FACEBOOK);
	}

	public void btnTW_Click(View view) {
		adapter.authorize(LoginActivity.this, Provider.TWITTER);
	}

	public void btnGOOGLE_Click(View view) {
		adapter.authorize(LoginActivity.this, Provider.GOOGLE);
	}
```

LoginCallback

```js
	private final class ResponseListener implements DialogListener {
		@Override
		public void onComplete(Bundle values) {
			if (progress != null)
				progress.dismiss();

			String providerName = values.getString(SocialAuthAdapter.PROVIDER);
			String token = General.adapter.getCurrentProvider().getAccessGrant().getKey();

			if (General.adapter != null)
				if (General.adapter.getUserProfile() != null) {
					userEmail = General.adapter.getUserProfile().getEmail();
					userDisplayName = General.adapter.getUserProfile().getDisplayName();
					userSocialID = General.adapter.getUserProfile().getValidatedId();
.
.
.
}
```

<span style="color: #ff0000;">**10-02-2014 (tested with socialauth v.3.1 and working)**</span>
**twitter settings**

Permissions = Tested with ReadOnly (working)
Settings  =  'Allow this application to be used to Sign in with Twitter' must be checked
Settings - CallbackURL = must specified (even the url doesnt exist)

## Using socialauth-4.9.jar + socialauth-android-3.2.jar

<span style="color: #ff0000;">**13-02-2016**

Today I started a PRJ, needs Facebook integration, new homepage discovered for socialauth at github - great!.
[https://github.com/3pillarlabs/socialauth-android/](https://github.com/3pillarlabs/socialauth-android/)

All plugged! Ooops the problem? Doesnt return the user email, email is null! :(

digging - I found a reply with a solution from #PHP library for Facebook# [https://github.com/mkdynamic/omniauth-facebook/issues/61#issuecomment-135767430](https://github.com/mkdynamic/omniauth-facebook/issues/61#issuecomment-135767430)

Finally, I patched the **socialauth-4.9.jar** to make it appear! fill free to use the lib :

[https://www.mediafire.com/?4y1h5tofbigp5he](https://www.mediafire.com/?4y1h5tofbigp5he)

guide for linkedin - tested and working - [http://www.3pillarglobal.com/insights/part-2-using-socialauth-to-integrate-linkedin-api-in-android](http://www.3pillarglobal.com/insights/part-2-using-socialauth-to-integrate-linkedin-api-in-android)

Login callback revised
```js
	private final class ResponseListener implements DialogListener {
		@Override
		public void onComplete(Bundle values) {
			// https://developers.facebook.com/docs/android/downloads
			// https://developers.facebook.com/docs/facebook-login/android
			// https://developers.facebook.com/docs/facebook-login/permissions
			// https://developers.facebook.com/docs/android/change-log-4.x
			// FYI : last version of FacebookSDK on JAR flavor is facebook-android-sdk-4.5.1

			if (General.adapter != null) 
				General.adapter.getUserProfileAsync(new ProfileDataListener());
		}
	}

	private final class ProfileDataListener implements SocialAuthListener {

		@Override
		public void onExecute(String providerName, Object arg1) {
			if (arg1==null)
				return;

			org.brickred.socialauth.Profile u = (org.brickred.socialauth.Profile) arg1;

			String user_mail = General.adapter.getUserProfile().getEmail();
			String user_name = null;
			int login_way = 0;

			if (providerName.equalsIgnoreCase("facebook")) {
				if (u.getFullName() != null)
					user_name = u.getFullName();
				else if (u.getValidatedId() != null)
					user_name = u.getValidatedId();
				else
					user_name = "**isnull**";

				login_way = 2;
			} else if (providerName.equalsIgnoreCase("linkedin")) {
				user_name = u.getDisplayName();

				if (user_name == null) {
					if (u.getFirstName() != null && u.getLastName() != null)
						user_name = u.getFirstName() + u.getLastName();
					else if (u.getFirstName() != null)
						user_name =u.getFirstName();
					else if (u.getLastName() != null)
						user_name = u.getLastName();
					else
						user_name = "**isnull**";
				}

				login_way = 3;
			}

			//app custom function
			store_social_info(user_mail, user_name, login_way);
		}

		private void store_social_info(String user_mail, String user_name, int login_way) {
			if (!General.checkNetworkConnection(LoginActivity.this, true))
				return;

		}
	}
```

<span style="color: #ff0000;">**16-02-2016 - sayantam (3Pillar Global) answered**</span>

> Please upgrade to socialauth 4.11. You can get the jar from Maven or Sourceforge.

wow!

[http://mvnrepository.com/artifact/org.brickred/socialauth](http://mvnrepository.com/artifact/org.brickred/socialauth)

<span style="color: #ff0000;">**02-11-2016 - Checking with AndroidStudio v2.2**</span>

Download AAR from http://mvnrepository.com/artifact/org.brickred/socialauth-android
Download JAR from (main java lib) http://mvnrepository.com/artifact/org.brickred/socialauth

goto File > New > Module > Import these two^

make sure at **build.gradle (Module:app)**
```js
//https://github.com/3pillarlabs/socialauth-android/issues/93#issuecomment-222129829
dependencies {
    compile fileTree(include: ['*.jar'], dir: 'libs')
    compile('org.brickred:socialauth-android:3.2.1'){
        exclude module: 'socialauth'
    }
```

thats it!</span>

origin - http://www.pipiscrew.com/?p=788 socialauth-android