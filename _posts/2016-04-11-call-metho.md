---
title: call method exists in fragment from actiobar settings
author: PipisCrew
date: 2016-04-11
categories: [android]
toc: true
---

source - [http://stackoverflow.com/a/22182746/1320686](http://stackoverflow.com/a/22182746/1320686)

```js
//activity_main.xml
<android.support.v4.widget.drawerlayout xmlns:android="http://schemas.android.com/apk/res/android" android:id="@+id/drawer_layout" android:layout_width="match_parent" android:layout_height="match_parent">

    <framelayout android:id="@+id/frame_container" android:layout_width="match_parent" android:layout_height="match_parent"></framelayout>

    <listview android:id="@+id/list_slidermenu" android:layout_width="240dp" android:layout_height="match_parent" android:layout_gravity="start" android:choicemode="singleChoice" android:divider="#272727" android:dividerheight="1dp" android:listselector="@drawable/list_selector" android:background="#303030"></listview>
</android.support.v4.widget.drawerlayout>

//menu > main.xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/action_test" android:orderincategory="100" android:showasaction="never" android:title="@string/action_test"></item>
    <item android:id="@+id/action_pipiscrew" android:orderincategory="100" android:showasaction="never" android:title="@string/pipiscrew"></item>
</menu>
```

```js
//activity_main.java
	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
		getMenuInflater().inflate(R.menu.main, menu);
		return true;
	}

	@Override
	public boolean onOptionsItemSelected(MenuItem item) {
		// toggle nav drawer on selecting action bar app icon/title
		if (mDrawerToggle.onOptionsItemSelected(item)) {
			return true;
		}

		// Handle action bar actions click
		switch (item.getItemId()) {
		case R.id.action_test:
			test();
			return true;
		default:
			return super.onOptionsItemSelected(item);
		}
	}

	private void test()
	{ 
		//is a test!
		Fragment currentFragment = getFragmentManager().findFragmentById(R.id.frame_container);

		if (currentFragment instanceof my_fragment) {
			my_fragment x = (my_fragment) currentFragment;
			x.pipiscrew_method();
		}
	}
```	

```js
//my_fragment.java
	@Override
	public void onActivityCreated(Bundle savedInstanceState) {
		super.onActivityCreated(savedInstanceState);

		//Report that this fragment would like to participate in populating the options menu by receiving a call  -  http://developer.android.com/reference/android/app/Fragment.html
		setHasOptionsMenu(true);
	}

	@Override
	public boolean onOptionsItemSelected(MenuItem item) {

		// Handle action bar actions click
		switch (item.getItemId()) {
		case R.id.action_pipiscrew:
			pipiscrew_method();
			return true;
		default:
			return super.onOptionsItemSelected(item);
		}
	}

	private void pipiscrew_method()
	{ 
		//is pipiscrew_method!
	}
```

origin - http://www.pipiscrew.com/?p=4206 android-call-method-exists-in-fragment-from-actiobar-settings