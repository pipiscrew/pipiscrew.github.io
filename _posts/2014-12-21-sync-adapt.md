---
title: Sync Adapter
author: PipisCrew
date: 2014-12-21
categories: []
toc: true
---

[http://developer.android.com/training/sync-adapters/creating-sync-adapter.html](http://developer.android.com/training/sync-adapters/creating-sync-adapter.html)

[http://udinic.wordpress.com/2013/07/24/write-your-own-android-sync-adapter/](http://udinic.wordpress.com/2013/07/24/write-your-own-android-sync-adapter/) *OR* [https://github.com/Udinic/SyncAdapter](https://github.com/Udinic/SyncAdapter)

[http://www.slideshare.net/AlexTumanoff/android-sync-adapter](http://www.slideshare.net/AlexTumanoff/android-sync-adapter)

http://www.vogella.com/tutorials/AndroidSQLite/article.html#contentprovider_overview

[http://chariotsolutions.com/blog/post/android-data-sync/](http://chariotsolutions.com/blog/post/android-data-sync/) (source [http://codehighway.postach.io/android-data-sync](http://codehighway.postach.io/android-data-sync))

http://www.manning.com/sessa/50AH_Sample05.pdf

http://naked-code.blogspot.gr/2011/05/revenge-of-syncadapter-synchronizing.html

http://www.c99.org/2010/01/23/writing-an-android-sync-provider-part-1/comment-page-1/

http://github.com/vseguip/Sweet

> What is a content provider?

A SQLite database is private to the application which creates it. If you want to share data with other applications you can use a content provider (short provider).

A provider allows applications to access data. In most cases this data is stored in an SQlite database.

While a content provider can be used within an application to access data, its is typically used to share data with other application. As application data is by default private, a content provider is a convenient to share you data with other application based on a structured interface.

A content provider must be declared in the AndroidManifest.xml file.

[http://www.tutorialspoint.com/android/android_content_providers.htm](http://www.tutorialspoint.com/android/android_content_providers.htm)
[http://www.techotopia.com/index.php/An_Android_Content_Provider_Tutorial](http://www.techotopia.com/index.php/An_Android_Content_Provider_Tutorial)
[http://www.mysamplecode.com/2012/11/android-database-content-provider.html](http://www.mysamplecode.com/2012/11/android-database-content-provider.html)

**generators**
[http://github.com/Trikke/android-sqlite-generator](http://github.com/Trikke/android-sqlite-generator)
[http://github.com/novoda/sqlite-provider](http://github.com/novoda/sqlite-provider)
[http://github.com/BoD/android-contentprovider-generator](http://github.com/BoD/android-contentprovider-generator)
[http://github.com/mediarain/RoboCoP](http://github.com/mediarain/RoboCoP)
[BambooStorage](https://android-arsenal.com/tag/20)

> SyncAdapter

<strong style="color:red;">SyncResult** by 43matthew - source [http://stackoverflow.com/a/17354811](http://stackoverflow.com/a/17354811)

The **SyncResult** object has a **delayUntil** field that you can set from your sync adapter which will delay each following sync by the specified number of seconds.

Otherwise, the sync **will be rescheduled** if

SyncResult.**madeSomeProgress()** returns true - i.e. some work was successfully accomplished by the sync (corresponding to stats.numDeletes, stats.numInserts > 0, stats.numUpdates > 0) SyncResult.**hasSoftError()** returns true - i.e. it failed due to an IOException or because SyncResult.syncAlreadyInProgress was true.

The sync adapter can set SyncResult.**tooManyRetries = true** which will indicate to the SyncManager **that the sync is not to rescheduled**

<strong style="color:red;">PeriodicSync** by Christopher Alexander - source [http://digitalassassin.net/2014/03/contentresolver-addperiodicsync-doesnt-work-never-syncs/](http://digitalassassin.net/2014/03/contentresolver-addperiodicsync-doesnt-work-never-syncs/)

1)You must call ContentResolver.**setSyncAutomatically** with true as the third (sync) parameter to enable syncing for your adaptor.
2)The fourth (pollFrequency) parameter of ContentResolver.**addPeriodicSync** is a number of seconds, as stated here, and not milliseconds, as implied in the training guide. The demo code for addPeriodicSync in the training guide will cause a sync once every thousand hours instead of once an hour. aka 
```js
//http://developer.android.com/training/sync-adapters/running-sync-adapter.html#RunPeriodic
//http://commondatastorage.googleapis.com/androiddevelopers/shareables/training/BasicSyncAdapter.zip

//SyncUtils.java
Line  33 -     private static final long SYNC_FREQUENCY = 60 * 60;
```

sync every 3mins :
```js
ContentResolver.setIsSyncable(mConnectedAccount, AutomotoServiceContentProvider.AUTHORITY, 1);
ContentResolver.setSyncAutomatically(mConnectedAccount, AutomotoServiceContentProvider.AUTHORITY, true);
ContentResolver.addPeriodicSync(mConnectedAccount, AutomotoServiceContentProvider.AUTHORITY, bnd, 180);
```

trigger refresh by application option (cutted frlyom official android example)
```js
	public void TriggerRefresh() {
		Bundle b = new Bundle();
		// Disable sync backoff and ignore sync preferences. In other words...perform sync NOW!
		b.putBoolean(ContentResolver.SYNC_EXTRAS_MANUAL, true);
		b.putBoolean(ContentResolver.SYNC_EXTRAS_EXPEDITED, true);
		ContentResolver.requestSync(mConnectedAccount, // Sync account
				AutomotoServiceContentProvider.AUTHORITY, // Content authority
				b); // Extras
	}
```</strong></strong>

origin - http://www.pipiscrew.com/?p=1825 android-sync-adapter