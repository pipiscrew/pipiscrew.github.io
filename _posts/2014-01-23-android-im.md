---
title: Android implement Push Notification system
author: PipisCrew
date: 2014-01-23
categories: []
toc: true
---

start points :
http://developer.android.com/google/gcm/index.html
http://developer.android.com/google/gcm/gs.html
First, install ‘Google Play services’ through **SDK Manager.exe** is under **Extras**

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap278s.jpg "snap278s")

This one will download a library project called **google-play-services_lib** exists at :

C:\you_androidSDK_path\extras\google\google_play_services\libproject

Go  to eclipse and import this library project!

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap279s.jpg "snap279s")

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap282s.jpg "snap282s")

**<span style="text-decoration: underline;">Warning you must check ‘Copy project into workspace’</span>**

otherwise will not work because the path is too long.

after succefully import, goto library manifest and replace with this tag

```js
    <uses-sdk android:minsdkversion="16"></uses-sdk>
```

restart eclipse!

Sign in with your google account to [https://cloud.google.com/console](https://cloud.google.com/console)

And create a new Project, you will get a **Project ID** and a  **Project Number**

We will use the **Project Number** later as sender-id..

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap274s.jpg "snap274s")

Enable the **Google Cloud Messaging for Android** (only this needed to be turned on) at **API**

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap275s.jpg "snap275s")

# <span style="color: #ff0000;">**[update 23/1/2014]**</span>

Google Developer Console change, there is a secret when creating ServerKey!

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap575.png "snap575")

when you are here and Press 'Create New Key' 1st modal appears asking for which purpose when choosing **Server** 2nd modal appears asking to

write your server IP! dont do anything! just leave black the editbox and press Create!!!! <span style="color: #0000ff;"> **live your myth with GOOGLE!**</span>

FYI :

Registered Apps made Credentials

--

**new sample** -- [https://github.com/GoogleCloudPlatform/solutions-mobile-backend-starter-android-client](https://github.com/GoogleCloudPlatform/solutions-mobile-backend-starter-android-client "https://github.com/GoogleCloudPlatform/solutions-mobile-backend-starter-android-client")

# <span style="color: #ff0000;">**[update 23/1/2014]**</span>

Goto **Registered Apps** and create a new one choosing platform Web Application. will we use later the **Server Key - Api Key** at PHP implementation

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap320.png "snap320")

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap321.png "snap321")

Goto **Registered Apps** and create a new one.

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap277s.jpg "snap277s")

You can find the sign-key SHA1 at Eclipse > Window > Preferences (warning this is for debug only, you have to update it, when make the real build)

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap276s.jpg "snap276s")

In general you reveal it also with a simple command line (when ask for password type **android**) :

keytool -exportcert -alias androiddebugkey -keystore C:\Users\you_user_name\.android\debug.keystore -list –v
pause

We create a test android project

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap273.png "snap273")

That makes a reference  to  library project called **google-play-services_lib** (that already imported into workspace)

We select the new project > r-click > properties

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap288s.jpg "snap288s")

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap289s.jpg "snap289s")

Press ok, you will see the green tick.

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap290s.jpg "snap290s")

So now the new project has dependencies right?

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap291.png "snap291")

In next we have to set the proper permissions in manifest file :

As described at [http://developer.android.com/google/gcm/client.html](http://developer.android.com/google/gcm/client.html) so I add these lines

```js
    <uses-permission android:name="android.permission.INTERNET"></uses-permission>
    <uses-permission android:name="android.permission.GET_ACCOUNTS"></uses-permission>
    <uses-permission android:name="android.permission.WAKE_LOCK"></uses-permission>
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE"></uses-permission>

    <permission android:name="com.example.toto.permission.C2D_MESSAGE" android:protectionlevel="signature"></permission>
    <uses-permission android:name="com.example.toto.permission.C2D_MESSAGE"></uses-permission>
```

Next we go to

[http://code.google.com/p/gcm/source/browse/gcm-client/src/com/google/android/gcm/demo/app/DemoActivity.java](http://code.google.com/p/gcm/source/browse/gcm-client/src/com/google/android/gcm/demo/app/DemoActivity.java)

and copy & paste the code!

First the public vars :

```js
    public static final String EXTRA_MESSAGE = "message";
    public static final String PROPERTY_REG_ID = "registration_id";
    private static final String PROPERTY_APP_VERSION = "appVersion";
    private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;

    /**
     * Substitute you own sender ID here. This is the project number you got
     * from the API Console, as described in "Getting Started."
     */
    String SENDER_ID = "Your-Sender-ID";

    /**
     * Tag used on log messages.
     */
    static final String TAG = "GCM Demo";

    TextView mDisplay;
    GoogleCloudMessaging gcm;
    AtomicInteger msgId = new AtomicInteger();
    Context context;

    String regid;
```

After paste > press CTRL+SHIFT+O to make the auto import, replace SENDER_ID variable with your application **Project Number**

Then the other procedures, ok done, first run :

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/Snap292s.jpg "Snap292s")

Oops I got :

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap293.png "snap293")wtf? google doesnt say anything about this!?

Go to manifest and paste this inside application tag!

```js
        </meta-data>
```

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap295s.jpg "snap295s")

Re-run! Works!

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/Snap296n.png "Snap296n")

---------------------------------------------------

Continuing to implement the **WakefulBroadcastReceiver** (GcmBroadcastReceiver)
[http://code.google.com/p/gcm/source/browse/gcm-client/src/com/google/android/gcm/demo/app/GcmBroadcastReceiver.java](http://code.google.com/p/gcm/source/browse/gcm-client/src/com/google/android/gcm/demo/app/GcmBroadcastReceiver.java)

I copy the source to my application, but I got an error in imports about

android.support.v4.content.WakefulBroadcastReceiver

seems need

C:\androidSDK_path\extras\android\support\v4\android-support-v4.jar

Fire up SDK.exe and download :

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap299s.jpg "snap299s")

Then drop it to folder **libs**

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap300.png "snap300")

then I go to my application manifest and merge from ([http://developer.android.com/google/gcm/client.html](http://developer.android.com/google/gcm/client.html))

```js
        <receiver android:name=".GcmBroadcastReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"></action>
                <category android:name="com.example.toto"></category>
            </intent-filter>
        </receiver>
        <service android:name=".GcmIntentService"></service>
```

Continuing to implement the **IntentService (GcmIntentService)**

[http://code.google.com/p/gcm/source/browse/gcm-client/src/com/google/android/gcm/demo/app/GcmIntentService.java](http://code.google.com/p/gcm/source/browse/gcm-client/src/com/google/android/gcm/demo/app/GcmIntentService.java)

---------------------------------------------------

now, after you get a deviceID (aka use your mobile), create a sample PHP file using curl to post variables at google server, you first test!

```js
<?php replace="" with="" real="" server="" key=""?> API key from Google Cloud Console
$apiKey = "xx-03HLEiyj1_l9Aim3I2Gmps";

// Replace with real client registration IDs (aka mobile)
$registrationIDs = array( "asddasdQDD9GoCQyAoz-vH2rqstB5zIIl7UoMCvJ-90vWmyMXBH8T5EcvYtI3JnuwDIeN9w" );

// Message to be sent
$message = "pipiscrew";

// Set POST variables
$url = 'https://android.googleapis.com/gcm/send';

$fields = array(
                'registration_ids'  => $registrationIDs,
                'data'              => array( "message" => $message ),
                );

$headers = array(
                    'Authorization: key=' . $apiKey,
                    'Content-Type: application/json'
                );

// Open connection
$ch = curl_init();

// Set the url, number of POST vars, POST data
curl_setopt( $ch, CURLOPT_URL, $url );

curl_setopt( $ch, CURLOPT_POST, true );
curl_setopt( $ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );

curl_setopt( $ch, CURLOPT_POSTFIELDS, json_encode( $fields ) );

// Execute post
$result = curl_exec($ch);

// Close connection
curl_close($ch);

echo $result;
?>

```

workssss!

<span style="color: #ff0000;">**--stop reading-------OLD before using Registered Apps > Server--------stop reading----------OLD before using Registered Apps > Server---**</span>

All done going for PHP Server implementation, after some 0's
**Unauthorized**

Error 401

I realize the server have to be on whitelist :
1-
https://www.google.com/webmasters/tools
2-
Google Cloud Console
API & Auth > Notification endpoints

references :
http://developer.android.com/google/gcm/http.html
http://stackoverflow.com/questions/11242743/gcm-with-php-google-cloud-messaging
http://distriqt.com/post/1223
http://www.robertprice.co.uk/robblog/2013/02/posting-json-to-a-web-service-with-php/
http://github.com/Redth/PushSharp
http://twisted.dyndns.tv:3194/DevForums/viewtopic.php?t=63#p181

**Note:** If your organization has a firewall that restricts the traffic to or from the Internet, you need to configure it to allow connectivity with GCM in order for your Android devices to receive messages. The ports to open are: 5228, 5229, and 5230. GCM typically only uses 5228, but it sometimes uses 5229 and 5230. GCM doesn't provide specific IPs, so you should allow your firewall to accept outgoing connections to all IP addresses contained in the IP blocks listed in Google's ASN of 15169.

**************************************** NOOOOOOOOOOOOOOOOOO

the only solution is to go at Google old console mode, by going to https://code.google.com/apis/console/b/0/?noredirect

or by clicking Go back

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap309.png "snap309")

then there, click the Create new Project big button!

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap312.png "snap312")

now the **Project Number** is in URL

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap3101.png "snap310")

then natigate to **API Access** to get the API key for PHP + manipulate **Notification Endpoints**
![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap3131.png "snap313")

and dont forget to enable **Google Cloud Messaging for Android** under **Services**

![](https://www.pipiscrew.com/wp-content/uploads/2013/12/snap314.png "snap314")

origin - http://www.pipiscrew.com/?p=529 android-implement-push-notification-system