---
title: Android Global Exception Handler
author: PipisCrew
date: 2014-01-09
categories: []
toc: true
---

//**use only on main activity**

```js
public class listnotes extends BaseActivity {
}
```

//**AndroidManifest.xml**

```js

<activity android:name="com.example.pipiscrewnotes.CrashActivity" android:label="Crash">
        </activity>
```

//**crashreport.xml**

```js
<?xml version="1.0" encoding="utf-8"?>
<linearlayout xmlns:android="http://schemas.android.com/apk/res/android" android:orientation="vertical" android:layout_width="fill_parent" android:layout_height="fill_parent">

    <relativelayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_height="wrap_content" android:orientation="horizontal" android:layout_width="fill_parent">

        <textview android:id="@+id/lblCrashed" android:layout_width="match_parent" android:layout_height="50dp" android:textcolor="#ff5158" android:gravity="center" android:text="JUST CRASHED!" android:background="#000000" android:textsize="30dp" android:textstyle="bold"></textview>

        <button android:id="@+id/btnSend" android:layout_alignparentright="true" android:layout_height="wrap_content" android:layout_width="wrap_content" android:textsize="10dp" android:text="send error" android:onclick="btnSend_Click"></button>

    </relativelayout>

    <scrollview android:layout_width="fill_parent" android:layout_height="fill_parent" android:fillviewport="true" android:layout_weight="1.0" android:fadingedgelength="0dp">

        <textview android:id="@+id/txtCrash" android:layout_width="fill_parent" android:layout_height="match_parent" android:inputtype="textMultiLine|textNoSuggestions" android:textcolor="#ffffff" android:background="#000000" android:gravity="top"></textview>
    </scrollview>
</linearlayout>
```

//**CrashAcitivity.java**

```js
package com.example.pipiscrewnotes;

import android.app.Activity;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

public class CrashActivity extends Activity {

    public void onCreate(Bundle icicle) {
        super.onCreate(icicle);

        setContentView(R.layout.crashreport);

        final String stackTrace = getIntent().getStringExtra("stacktrace");
        final TextView reportTextView = (TextView) findViewById(R.id.txtCrash);
        reportTextView.setText(stackTrace);
    }

    public void btnSend_Click(View view) {
        final TextView t = (TextView) findViewById(R.id.txtCrash);

        Intent emailIntent = new Intent(Intent.ACTION_SENDTO, Uri.fromParts(
                "mailto", "pipis@jmail.com", null));
        emailIntent.putExtra(Intent.EXTRA_SUBJECT, "PipisCrew Notes Crash Report");
        emailIntent.putExtra(Intent.EXTRA_TEXT, t.getText().toString());
        startActivity(Intent.createChooser(emailIntent, "Send error to author..."));
    }
}
```

**//BaseActivity.java** 

```js
package com.example.pipiscrewnotes;

import android.app.Activity;
import android.content.Intent;
import android.os.Build;
import android.os.Bundle;
public class BaseActivity extends Activity {
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		Thread.setDefaultUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {
			@Override
			public void uncaughtException(Thread paramThread, Throwable e) {

				final String DOUBLE_LINE_SEP = "\r\n\r\n";
				final String SINGLE_LINE_SEP = "\r\n";
				StackTraceElement[] arr = e.getStackTrace();
				final StringBuffer report = new StringBuffer(e.toString());
				final String lineSeperator = "-------------------------------\n\n";
				report.append(DOUBLE_LINE_SEP);
				report.append("--------- Stack trace ---------\n\n");
				for (int i = 0; i < arr.length;="" i++)="" {="" report.append("="" ");="" report.append(arr[i].tostring());="" report.append(single_line_sep);="" }="" if="" the="" exception="" was="" thrown="" in="" a="" background="" thread="" inside="" asynctask,="" then="" the="" actual="" exception="" can="" be="" found="" with="" getcause="" throwable="" cause="e.getCause();" if="" (cause="" !="null)" {="" report.append(lineseperator);="" report.append("---------="" cause="" ---------\n\n");="" report.append(cause.tostring());="" report.append(double_line_sep);="" arr="cause.getStackTrace();" for="" (int="" i="0;" i="">< arr.length;="" i++)="" {="" report.append("="" ");="" report.append(arr[i].tostring());="" report.append(single_line_sep);="" }="" }="" getting="" the="" device="" brand,model="" and="" sdk="" verion="" details.="" report.append(lineseperator);="" report.append("---------="" device="" ---------\n\n");="" report.append("brand:="" ");="" report.append(build.brand);="" report.append(single_line_sep);="" report.append("device:="" ");="" report.append(build.device);="" report.append(single_line_sep);="" report.append("model:="" ");="" report.append(build.model);="" report.append(single_line_sep);="" report.append("metric:="" ");="" int="" density="getResources().getDisplayMetrics().densityDpi;" switch="" (density)="" {="" case="" displaymetrics.density_low:="" report.append("ldpi="" ");="" break;="" case="" displaymetrics.density_medium:="" report.append("mdpi="" ");="" break;="" case="" displaymetrics.density_high:="" report.append("hdpi="" ");="" break;="" case="" displaymetrics.density_xhigh:="" report.append("xhdpi="" ");="" break;="" }="" displaymetrics="" dm="new" displaymetrics();="" getwindowmanager().getdefaultdisplay().getmetrics(dm);="" report.append(string.valueof(dm.widthpixels)="" +="" "x"="" +="" string.valueof(dm.heightpixels)="" +="" "="" "="" +="" string.valueof(dm.densitydpi)="" +="" "dpi")="" ;="" report.append(single_line_sep);="" report.append("id:="" ");="" report.append(build.id);="" report.append(single_line_sep);="" report.append("product:="" ");="" report.append(build.product);="" report.append(single_line_sep);="" report.append(lineseperator);="" report.append("---------="" firmware="" ---------\n\n");="" report.append("sdk:="" ");="" report.append(build.version.sdk);="" report.append(single_line_sep);="" report.append("release:="" ");="" report.append(build.version.release);="" report.append(single_line_sep);="" report.append("incremental:="" ");="" report.append(build.version.incremental);="" report.append(single_line_sep);="" report.append(lineseperator);="" intent="" crashedintent="new" intent(baseactivity.this,="" crashactivity.class);="" crashedintent.putextra("stacktrace",="" report.tostring());="" crashedintent.addflags(intent.flag_activity_clear_when_task_reset);="" crashedintent.addflags(intent.flag_activity_clear_top);="" startactivity(crashedintent);="" system.exit(0);="" }="" });="" }="" }="" ```="">  

![](https://www.pipiscrew.com/wp-content/uploads/2013/08/androidGlobalErrorHandler.jpg "androidGlobalErrorHandler")

origin - http://www.pipiscrew.com/?p=416 android-global-exception-handler