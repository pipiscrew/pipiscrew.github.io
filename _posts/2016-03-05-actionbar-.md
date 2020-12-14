---
title: ActionBar use it for back
author: PipisCrew
date: 2016-03-05
categories: [android]
toc: true
---

```js
//values.xml
    //add this
    <style name="AppBaseThemeActionBar" parent="android:Theme.Holo.Light.DarkActionBar">
        <item name="android:windowNoTitle">false</item>
    </style>
    //add this

    <style name="AppBaseTheme" parent="android:Theme.Holo.Light">
        <item name="android:windowNoTitle">true</item>
    </style>

    <style name="AppTheme" parent="AppBaseTheme">
        <item name="android:windowNoTitle">true</item>
    </style>
```

```js
        <activity android:name=".Product_Detail" android:parentactivityname="com.x.x.MainActivity">> android:theme="@android:style/Theme.Holo.Light.DarkActionBar"
            android:label="@string/title_activity_product__detail" >
        </activity>
```

when activity is sure that called from one parent, there is a xml property (line3^). No code needed... click&return :)

```js
public class Product_Detail extends Activity {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_product_detail);

		getActionBar().setHomeButtonEnabled(true);
		getActionBar().setDisplayHomeAsUpEnabled(true);
	}

	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
		// Inflate the menu; this adds items to the action bar if it is present.
		getMenuInflater().inflate(R.menu.product__detail, menu);
		return true;
	}
```

otherwise you can use the classic way :
```js
	@Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()) {
            case android.R.id.home:
                // app icon in action bar clicked; goto parent activity.
                this.finish();
                return true;
            default:
                return super.onOptionsItemSelected(item);
        }
    }
```

![Snap155](https://www.pipiscrew.com/wp-content/uploads/2016/03/Snap155.png)

## customize the appbar logo

In AndroidManifest.xml add line: android:logo="@drawable/logo"

<application android:allowbackup="true" android:icon="@drawable/ic_launcher" android:logo="@drawable/logo" test="" made,="" add="" a="" picture="" 128x34="" looks="" nice!=""></application>

## customize the text

getActionBar().setTitle("test");   

## customizes

more [http://stackoverflow.com/a/3438352/1320686](http://stackoverflow.com/a/3438352/1320686)
generator - [http://jgilfelt.github.io/android-actionbarstylegenerator/](http://jgilfelt.github.io/android-actionbarstylegenerator/)
```js
@Override
public void setActionBar(String heading) {
    // TODO Auto-generated method stub

    com.actionbarsherlock.app.ActionBar actionBar = getSupportActionBar();
    actionBar.setHomeButtonEnabled(true);
    actionBar.setDisplayHomeAsUpEnabled(false);
    actionBar.setDisplayShowHomeEnabled(false);
    actionBar.setBackgroundDrawable(new ColorDrawable(getResources().getColor(R.color.title_bar_gray)));
    actionBar.setTitle(heading);
    actionBar.show();

}
```

origin - http://www.pipiscrew.com/?p=4224 android-actionbar-use-it-for-back