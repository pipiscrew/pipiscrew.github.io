---
title: Android implement G/FB/TW login via socialauth-android library
author: PipisCrew
date: 2017-02-26
categories: [android]
toc: true
---

Start points (requires go0gle plays services library) using Google+ :
[https://developers.google.com/+/mobile/android/sign-in](https://developers.google.com/+/mobile/android/sign-in)

This method described (dont require go0gle plays services, but needs a **3rd** party JARs (total filesize = 275kb)) :

ok,so we are again at Google Cloud Console (and we created a project) https://cloud.google.com/console
we have to create n **OAuth 2.0 client ID**

first enable from API menu the option **Google+ API**

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap341.png "snap341")

then goto **Registered apps** > select **Native** (I didnt try with other choices)

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap343.png "snap343")

this will result  a **Client Secret**

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap344.png "snap344")

download the socialauth-android [http://code.google.com/p/socialauth-android/](http://code.google.com/p/socialauth-android/)

you must include the 2jars and **oauth_consumer.properties** file into your project

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap345.png "snap345")

edit **oauth_consumer.properties** file write there the **Client Secret** (btw offers login to all social webistes, google is just 1 of them)

```js
 <uses-permission android:name="android.permission.INTERNET"></uses-permission>
 <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
```

```js
	SocialAuthAdapter adapter;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_login);

			// Add it to Library
			adapter = new SocialAuthAdapter(new ResponseListener());

			// Add providers
			adapter.addProvider(Provider.FACEBOOK, R.drawable.facebook);
			adapter.addProvider(Provider.TWITTER, R.drawable.twitter);
			adapter.addProvider(Provider.TWITTER, R.drawable.google);

			// Providers require setting user call Back url
			adapter.addCallBack(Provider.TWITTER, "http://socialauth.in/socialauthdemo/socialAuthSuccessAction.do");

	}

	public void btnFB_Click(View view) {
		adapter.authorize(LoginActivity.this, Provider.FACEBOOK);
	}

	public void btnTW_Click(View view) {
		adapter.authorize(LoginActivity.this, Provider.TWITTER);
	}

	public void btnGOOGLE_Click(View view) {
		adapter.authorize(LoginActivity.this, Provider.GOOGLE);
		//alternatively for Google+ you use Provider.GOOGLEPLUS
	}

	//socialauth-android listener
	private final class ResponseListener implements DialogListener {
		@Override
		public void onComplete(Bundle values) {
			String providerName = values.getString(SocialAuthAdapter.PROVIDER);
			String token = adapter.getCurrentProvider().getAccessGrant().getKey();

			if (adapter != null)
				if (adapter.getUserProfile() != null) {
					userEmail = adapter.getUserProfile().getEmail();
					userDisplayName = adapter.getUserProfile().getDisplayName();
					userSocialID = adapter.getUserProfile().getValidatedId();

					if (providerName.equalsIgnoreCase("facebook")) {
						if (token != null && userEmail != null && userSocialID != null) {
							//success login
							});
						} else
							General.mes(LoginActivity.this, "Unable to authenticate user");
					} else if (providerName.equalsIgnoreCase("google")) {

						if (token != null && userEmail != null && userSocialID != null) {
							//success login
							});
						} else
							General.mes(LoginActivity.this, "Unable to authenticate user");

					} else if (providerName.equalsIgnoreCase("twitter")) {
					//pipiscrew
					}
				}
		}

		@Override
		public void onError(SocialAuthError error) {
			Log.d("PipisCrew", "Authentication Error: " + error.getMessage());
		}

		@Override
		public void onCancel() {
			Log.d("PipisCrew", "Authentication Cancelled");
		}

		@Override
		public void onBack() {
			Log.d("PipisCrew", "Dialog Closed by pressing Back Key");
		}

	}
```

origin - http://www.pipiscrew.com/?p=592 android-implement-google-login-via-socialauth-android-library