---
title: push notification
author: PipisCrew
date: 2016-04-03
categories: [php,android]
toc: true
---

Alright, I develop an application for a client, is time to implement the push notification for one more time :)

At first download the latest **google-play-services** which is <b style="color:red">target:android-23**, seems that has some conflicts when tried to obfuscate it (using Eclipse / Android 6.0 for compile / ant) some of the errors :

```js

com.google.android.gms.internal.zzlh: can't find dynamically referenced class com.facebook.FacebookSdk

```

^wtf?

, whatever I restore back the <b style="color:red">target:android-16**!! **Plays 100%**

the steps : 

<b style="color:red">1-**On androidmanifest.xml add inside application tag :
```js
//androidmanifest.xml sample
<application android:name=".Dynomite" android:allowbackup="true" android:icon="@drawable/ic_launcher" android:label="@string/app_name" android:logo="@drawable/actionbar_logo_red" android:theme="@style/AppTheme">\

	<receiver android:name="com.test.gr.gcm.GcmBroadcastReceiver" android:permission="com.google.android.c2dm.permission.SEND">
		<intent-filter>

			<action android:name="com.google.android.c2dm.intent.RECEIVE"></action>

			<category android:name="com.test.gr"></category>
		</intent-filter>
	</receiver>
	<service android:name="com.test.gr.gcm.GcmIntentService"></service>

</application>
```

![snap120](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap120.png)

then add the needed files for into separate package I will name it gcm, so we have **com.text.gr.gcm**

```js
//GcmBroadcastReceiver.java
package com.test.gr.gcm;

import android.app.Activity;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.support.v4.content.WakefulBroadcastReceiver;

/**
 * This {@code WakefulBroadcastReceiver} takes care of creating and managing a
 * partial wake lock for your app. It passes off the work of processing the GCM
 * message to an {@code IntentService}, while ensuring that the device does not
 * go back to sleep in the transition. The {@code IntentService} calls
 * {@code GcmBroadcastReceiver.completeWakefulIntent()} when it is ready to
 * release the wake lock.
 */

public class GcmBroadcastReceiver extends WakefulBroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        // Explicitly specify that GcmIntentService will handle the intent.
        ComponentName comp = new ComponentName(context.getPackageName(), GcmIntentService.class.getName());
        // Start the service, keeping the device awake while it is launching.
        startWakefulService(context, (intent.setComponent(comp)));
        setResultCode(Activity.RESULT_OK);
    }
}

//GcmIntentService.java
package com.test.gr.gcm;

import android.app.IntentService;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.content.Context;
import android.content.Intent;
import android.content.SharedPreferences;
import android.graphics.BitmapFactory;
import android.media.RingtoneManager;
import android.net.Uri;
import android.os.Bundle;
import android.preference.PreferenceManager;
import android.support.v4.app.NotificationCompat;
import android.util.Log;

import com.google.android.gms.gcm.GoogleCloudMessaging;
import com.test.gr.MainActivity;
import com.test.gr.R;

/**
 * This {@code IntentService} does the actual handling of the GCM message.
 * {@code GcmBroadcastReceiver} (a {@code WakefulBroadcastReceiver}) holds a
 * partial wake lock for this service while the service does its work. When the
 * service is finished, it calls {@code completeWakefulIntent()} to release the
 * wake lock.
 */
public class GcmIntentService extends IntentService {
    public static final int NOTIFICATION_ID = 1;
    private NotificationManager mNotificationManager;
    NotificationCompat.Builder builder;

    public GcmIntentService() {
        super("GcmIntentService");
    }

    private SharedPreferences preferences;
    public static final String TAG = "GCM CC";

    @Override
    protected void onHandleIntent(Intent intent) {
        Bundle extras = intent.getExtras();
        GoogleCloudMessaging gcm = GoogleCloudMessaging.getInstance(this);
        // The getMessageType() intent parameter must be the intent you received
        // in your BroadcastReceiver.
        String messageType = gcm.getMessageType(intent);

        preferences = PreferenceManager.getDefaultSharedPreferences(getBaseContext());
        if (!extras.isEmpty()) {  // has effect of unparcelling Bundle
            /*
             * Filter messages based on message type. Since it is likely that GCM will be
             * extended in the future with new message types, just ignore any message types you're
             * not interested in, or that you don't recognize.
             */
            if (GoogleCloudMessaging.MESSAGE_TYPE_SEND_ERROR.equals(messageType)) {
                Log.d(TAG, "Send error: " + extras.toString());

            } else if (GoogleCloudMessaging.MESSAGE_TYPE_DELETED.equals(messageType)) {

                Log.d(TAG, "Deleted messages on server: " + extras.toString());
                // If it's a regular GCM message, do some work.
            } else if (GoogleCloudMessaging.MESSAGE_TYPE_MESSAGE.equals(messageType)) {

                // Post notification of received message.
                String title = extras.getString("title", null);
                String message = extras.getString("description", null);
                String link = extras.getString("link", null);

                sendNotification(title, message, link);

                Log.i(TAG, "Received: " + extras.toString());
            }
        }
        // Release the wake lock provided by the WakefulBroadcastReceiver.
        GcmBroadcastReceiver.completeWakefulIntent(intent);
    }

    // Put the message into a notification and post it.
    // This is just one simple example of what you might choose to do with
    // a GCM message.
    private void sendNotification(String title, String msg, String link) {
        mNotificationManager = (NotificationManager)
                this.getSystemService(Context.NOTIFICATION_SERVICE);

        Intent intent = new Intent(this, MainActivity.class);
        intent.putExtra("link", link);
        PendingIntent contentIntent = PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_CANCEL_CURRENT);

        NotificationCompat.Builder mBuilder = new NotificationCompat.Builder(this)
                .setLargeIcon(BitmapFactory.decodeResource(getBaseContext().getResources(), R.drawable.ic_launcher))
                .setSmallIcon(R.drawable.ic_launcher)
                .setContentTitle(title)
                .setStyle(new NotificationCompat.BigTextStyle()
                        .bigText(msg))
                .setContentText(msg);

        // Set the notification vibrate option
        if (preferences.getBoolean("notifications_new_message_vibrate", true)) {
            mBuilder.setVibrate(new long[]{1000, 1000, 1000, 1000, 1000});
        }
        // Set the notification ringtone
        if (preferences.getString("notifications_new_message_ringtone", null) != null) {
            mBuilder.setSound(Uri.parse(preferences.getString("notifications_new_message_ringtone", null)));
        } else {
            Uri alarmSound = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
            mBuilder.setSound(alarmSound);
        }

        // Show only if the notification are enabled
        if (preferences.getBoolean("notifications_new_message", true)) {
            mBuilder.setContentIntent(contentIntent);
            mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
    }
}
```

On your mainactivity (does matter if your application has a splashscreen, this will be added to mainactivity)

```js
//MainActivity.java
// GCM
public static final String PROPERTY_REG_ID = "notifyId";
private static final String PROPERTY_APP_VERSION = "1";
GoogleCloudMessaging gcm;
SharedPreferences preferences;
String reg_cgm_id;
static final String TAG = "MainActivity";

@Override
protected void onCreate(Bundle savedInstanceState) {
.
.
	// //////////////////////////////////////////////////////////////
	// GCM -
	if (checkPlayServices()) {
		gcm = GoogleCloudMessaging.getInstance(getApplicationContext());
		String reg_cgm_id = getRegistrationId(getApplicationContext());
		Log.i(TAG, "Play Services Ok.");
		if (reg_cgm_id == null || reg_cgm_id.isEmpty()) {
			Log.i(TAG, "Find Register ID.");
			registerInBackground();
		}
	} else {
		Log.i(TAG, "No valid Google Play Services APK found.");
	}
}

/**
 * Check the device to make sure it has the Google Play Services APK. If it
 * doesn't, display a dialog that allows users to download the APK from the
 * Google Play Store or enable it in the device's system settings.
 */
private boolean checkPlayServices() {
	int resultCode = GooglePlayServicesUtil.isGooglePlayServicesAvailable(MainActivity.this);
	if (resultCode != ConnectionResult.SUCCESS) {
		if (GooglePlayServicesUtil.isUserRecoverableError(resultCode)) {
			GooglePlayServicesUtil.getErrorDialog(resultCode, this, 9000).show();
		} else {
			Log.i(TAG, "This device is not supported.");
		}
		return false;
	}
	return true;
}

/**
 * Gets the current registration ID for application on GCM service.
 * If result is empty, the app needs to register.
 */
private String getRegistrationId(Context context) {
	String registrationId = General.get_pref(this).getString(PROPERTY_REG_ID, "");

	if (registrationId.isEmpty()) {
		Log.i(TAG, "Registration not found.");
		return "";
	}
	// Check if app was updated; if so, it must clear the registration ID
	// since the existing regID is not guaranteed to work with the new
	// app version.
	int registeredVersion = General.get_pref(this).getInt(PROPERTY_APP_VERSION, Integer.MIN_VALUE);
	int currentVersion = getAppVersion(context);
	if (registeredVersion != currentVersion) {
		Log.i(TAG, "App version changed.");
		return "";
	}
	return registrationId;
}

/**
 * Registers the application with GCM servers asynchronously.
 */
private void registerInBackground() {
	new AsyncTask<void, void,="" string="">() {
		@Override
		protected String doInBackground(Void... params) {
			String msg = "";
			try {
				if (gcm == null) {
					gcm = GoogleCloudMessaging.getInstance(MainActivity.this);
				}

				reg_cgm_id = gcm.register("**you project number**");

				msg = "Device registered, registration ID=" + reg_cgm_id;
				Log.d(TAG, "ID GCM: " + reg_cgm_id);

				// You should send the registration ID to your server
				sendRegistrationIdToBackend();

			} catch (IOException ex) {
				msg = "Error :" + ex.getMessage();
			}
			return msg;
		}

		@Override
		protected void onPostExecute(String msg) {

		}
	}.execute(null, null, null);
}

/**
 * Stores the registration ID and the app versionCode in the application SharedPreferences
 */
private void storeRegistrationId(Context context, String regId) {
	int appVersion = getAppVersion(context);
	Log.i(TAG, "Saving regId on app version " + appVersion);
	SharedPreferences.Editor editor = General.get_pref(this).edit();
	editor.putString(PROPERTY_REG_ID, regId);
	editor.putInt(PROPERTY_APP_VERSION, appVersion);
	editor.commit();
}

/**
 * Sends the registration ID to your server
 */
private void sendRegistrationIdToBackend() {
	//your own implementation to send the current device token (stored to public var reg_cgm_id) to your web server
	//only when server got it, call the
	storeRegistrationId(MainActivity.this, reg_cgm_id);
}

/**
 * @return Application's version code from the {@code PackageManager}.
 */
private static int getAppVersion(Context context) {
	try {
		PackageInfo packageInfo = context.getPackageManager().getPackageInfo(context.getPackageName(), 0);
		return packageInfo.versionCode;
	} catch (PackageManager.NameNotFoundException e) {
		// should never happen
		throw new RuntimeException("Could not get package name: " + e);
	}
}

```

## proguard rules

```js
//google-play-services_lib -- proguard-project.txt
-dontskipnonpubliclibraryclassmembers

-keep class * extends java.util.ListResourceBundle {
    protected Object[][] getContents();
}

# Keep SafeParcelable value, needed for reflection. This is required to support backwards
# compatibility of some classes.
-keep public class com.google.android.gms.common.internal.safeparcel.SafeParcelable {
    public static final *** NULL;
}

# Keep the names of classes/members we need for client functionality.
-keepnames @com.google.android.gms.common.annotation.KeepName class *
-keepclassmembernames class * {
    @com.google.android.gms.common.annotation.KeepName *;
}

# Needed for Parcelable/SafeParcelable Creators to not get stripped
-keepnames class * implements android.os.Parcelable {
    public static final ** CREATOR;
}

//com.test.gr -- proguard-project.txt
# Keel all googleclasses
-keep class com.google.** { *; }
-dontwarn com.google.**
```

## the steps for Google Cloud Platform

you go to [https://console.cloud.google.com/](https://console.cloud.google.com/), create a project, this project will taken a <b style="solor:red">Project Number** write it down!

![snap121](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap121.png)

goto <b style="solor:red">Enable and manage APIs** select the Mobile > Cloud messaging and enable it!
![snap122](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap122.png)

![snap123](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap123.png)

click credentials on ^left and create a server or browser key
[![snap124](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap124.png)](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap124.png)

I dont use the **Domain Verification** tab, I went to [https://www.google.com/webmasters/tools/home](https://www.google.com/webmasters/tools/home) click **add property** and verify by html file, my domain. In this way I can use Server and Browser keys....

at the time of the article 3/4/2016, my old application (https://www.pipiscrew.com/works/gcm-push-tested/), works, but send empty message on the device :
![snap127](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap127.png)

but lets 

## implement the PHP version!

```js
//index.php
<?php if="" ($_server['request_method']="==" 'post')="" {="" $password_string="mysql_escape_string($_POST[" password"]);"="" if="" ($password_string!="yourpasswordhere" )="" doesnt="" compare="" the="" mail="" {="" die("error!");="" }="" else="" {="" show="" the="" rest!="" }="" }="" else="" {="" login="" system=""?>

					<style>
					    body {
					      padding-top: 40px;
					      padding-bottom: 40px;
					      background-color: #eee;
					    }

					    .form-signin {
					      max-width: 330px;
					      padding: 15px;
					      margin: 0 auto;
					    }
					    .form-signin .form-signin-heading,
					    .form-signin .checkbox {
					      margin-bottom: 10px;
					    }
					    .form-signin .checkbox {
					      font-weight: normal;
					    }
					    .form-signin .form-control {
					      position: relative;
					      height: auto;
					      -webkit-box-sizing: border-box;
					         -moz-box-sizing: border-box;
					              box-sizing: border-box;
					      padding: 10px;
					      font-size: 16px;
					    }
					    .form-signin .form-control:focus {
					      z-index: 2;
					    }
					    .form-signin input[type="email"] {
					      margin-bottom: -1px;
					      border-bottom-right-radius: 0;
					      border-bottom-left-radius: 0;
					    }
					    .form-signin input[type="password"] {
					      margin-bottom: 10px;
					      border-top-left-radius: 0;
					      border-top-right-radius: 0;
					    }
					</style>

					    <div class="container">

					      <form class="form-signin" method="POST" action="">

## Please sign in

					        <label for="mail" class="sr-only">Email address</label>
					        <input type="email" name="mail" class="form-control" placeholder="Email address" required="" autofocus="">
					        <label for="password" class="sr-only">Password</label>
					        <input type="password" name="password" id="password" class="form-control" placeholder="Password" required="">

					        <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
					      </form>

					    </div> 

<?php exit;="" }=""?>

     <div class="container">
      <div class="header clearfix">

### Test - Push Panel

      </div>

      <div class="jumbotron">

# Send a push notification

       <form role="form" action="push_users.php" method="post">
  <div class="form-group">
    <label for="title">Title:</label>
    <input type="text" name="title" class="form-control" id="title">
  </div>
  <div class="form-group">
    <label for="msg">Message:</label>
    <input type="text" name="message" class="form-control" id="msg">
  </div>

  <button type="submit" class="btn btn-primary">Send now</button>
</form>
      </div>

    </div> 

//push_users.php
<?php date_default_timezone_set("utc");="" if="" (!$_post)="" die("use="" only="" post="" please");="" if(!isset($_post["title"])="" ||="" !isset($_post["message"]))="" die("no="" valid="" variables");="" require_once="" ('config.php');="" try="" {="" $db="connect_mysql();" }="" catch="" (exception="" $e)="" {="" die($e-=""?>getMessage());
}

$title = $_POST['title'];
$msg = $_POST['message'];

class GCM {
    function __construct(){}

    public function send_notification($registatoin_ids,$data) {

        // GOOGLE API KEY
        define("GOOGLE_API_KEY","your_server_key");
        $url="https://android.googleapis.com/gcm/send";
        $fields=array(
            "registration_ids"=>$registatoin_ids,
            "data"=>$data,
        );
        //var_dump($fields);
        $headers=array(
            "Authorization: key=".GOOGLE_API_KEY,
            "Content-Type: application/json"
        );
        $ch=curl_init();
        curl_setopt($ch,CURLOPT_URL,$url);
        curl_setopt($ch,CURLOPT_POST,true);
        curl_setopt($ch,CURLOPT_HTTPHEADER,$headers);
        curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
        curl_setopt($ch,CURLOPT_SSL_VERIFYPEER,false);
        curl_setopt($ch,CURLOPT_POSTFIELDS,json_encode($fields));
        $result_gcm=curl_exec($ch);
        if($result_gcm===FALSE){
            die("Curl failed: ".curl_error($ch));
        }
        curl_close($ch);

        var_dump($result_gcm); //for debug 
    }
}

//get user tokens by dbase records
$tokens = getSet($db,"select push_reg_id from users where push_reg_id IS NOT NULL",null);

if (!$tokens)
	die("there is no records");

$android_tokens = array();
$x=0;

foreach($tokens as $tok) {
	$android_tokens[] = $tok["push_reg_id"];
	$x++;
}

if ($android_tokens != array()) {
    $gcm=new GCM();
    $data=array("title"=>$title,"description"=>$msg,"link"=>$link);
    $result_android=$gcm->send_notification($android_tokens,$data);
}

?>

     <div class="container">
      <div class="header clearfix">

### Test - Push Panel

      </div>

      <div class="jumbotron">

# Good!

You have sent <?php echo="" $x;?=""?> push notification.

      </div>

    </div> 

```

source - [http://iconhandbook.co.uk/reference/chart/android/](http://iconhandbook.co.uk/reference/chart/android/)

[![snap128](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap128.png)](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap128.png)</b></b></void,></b></b></b>

origin - http://www.pipiscrew.com/?p=4720 android-push-notification