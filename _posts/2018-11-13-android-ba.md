---
title: Android backup wifi passwords needs androidos v6 and above
author: PipisCrew
date: 2018-11-13
categories: [android]
toc: true
---

<div>

Does anyone know how to recover saved WiFi passwords to a new Android smartphone?
https://productforums.google.com/d/msg/drive/Rt-L8TyjR54/YIXtioYAAwAJ
https://support.google.com/drive/answer/6305834?co=GENIE.Platform%3DAndroid&oco=1

Force Backup with ADB command

```js
src - https://forum.xda-developers.com/pixel-2-xl/how-to/forcing-pixel-2-xl-backup-t3691071
adb shell
bmgr run
bmgr backupnow --all
```

or (tested & working on S6)

```js
src - https://www.xda-developers.com/android-pie-test-manual-backup-google-drive/
adb devices  
adb shell bmgr backupnow --all
```

Back up phone - Samsung Galaxy J5
https://www.helpforsmartphone.com/public/en/samsung/galaxy-j5/android-5-1/guides/7/Back-up-phone-Samsung-Galaxy-J5

Sync, Back Up, and Restore Using Samsung Cloud
https://www.samsung.com/us/support/answer/ANS00060517/

-------

cutted from https://productforums.google.com/d/msg/drive/Rt-L8TyjR54/YIXtioYAAwAJ

If your device runs Android 6.0 and up, you can [back up](https://support.google.com/drive/answer/6305834?) and restore the following items on your Android [device](https://support.google.com/nexus/answer/2819582):

*   Apps

*   Call History

*   Device Settings

*   Contacts

*   Calendar

*   SMS (Pixel phones only)

*   Photos & videos (Pixel phones only)

<div>To turn on Backup, please follow the steps below:</div>
</div>
<div></div>
<div>

1.  Open your device's Settings app.

2.  Tap **System** ![and then](https://lh3.googleusercontent.com/nHFGZ_9xjCh-mP83zMzXQVJF5VYf2n6kwoBIxB2zv3V4VPT4gNTtBye8lYznogLqLPY=w13-h18 "and then") **Backup**.

3.  Turn on **Back up to Google Drive**.

<div>

When you add your Google Account to a device that's been set up, what you'd previously backed up for that Google Account gets put onto the device. To restore a backed-up account to a reset device, follow the on-screen steps. You can't restore a backup from a higher Android version onto a phone running a lower Android version. [Learn how to check and update your Android version](https://support.google.com/pixelphone/answer/4457705).

</div>
<div>

When you reinstall an app, you can restore app settings that you'd previously backed up with your Google Account.

To restore app settings:

1.  Open your device's Settings app.

2.  Tap **System** ![and then](https://lh3.googleusercontent.com/nHFGZ_9xjCh-mP83zMzXQVJF5VYf2n6kwoBIxB2zv3V4VPT4gNTtBye8lYznogLqLPY=w13-h18 "and then") **Backup** ![and then](https://lh3.googleusercontent.com/nHFGZ_9xjCh-mP83zMzXQVJF5VYf2n6kwoBIxB2zv3V4VPT4gNTtBye8lYznogLqLPY=w13-h18 "and then") **App data**.

3.  Turn on **Automatic restore**.

**Note:** Not all apps can back up or restore all settings and data.

* * *

Google Drive shot

![](https://i.imgur.com/kaNYOFY.jpg)

</div>
</div>

origin - http://www.pipiscrew.com/?p=14216 android-backup-wifi-passwords-needs-androidos-v6-and-above