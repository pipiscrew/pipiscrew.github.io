---
title: Android Indicator
author: PipisCrew
date: 2014-01-09
categories: []
toc: true
---

**// @ res/anim/my_indicator.xml**

```js
<rotate xmlns:android="http://schemas.android.com/apk/res/android" android:duration="2000" android:fillafter="false" android:fromdegrees="0" android:interpolator="@android:anim/linear_interpolator" android:pivotx="50%" android:pivoty="50%" android:repeatcount="infinite" android:startoffset="0" android:todegrees="-360"></rotate>

```

// @ activity

```js
    <imageview android:id="@+id/indicatorLbC" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_centerinparent="true" android:src="@drawable/indicator"></imageview>
```

// @ activity java

```js
	// indicator public var
	ImageView Indicator;

//	protected void onCreate(Bundle savedInstanceState) {
		//indicator
		Indicator = (ImageView) findViewById(R.id.indicatorLbC);
		startIndicator();

	public void startIndicator() {
		RotateAnimation rotation = new RotateAnimation(0f, 360f, Animation.RELATIVE_TO_SELF, 0.5f, Animation.RELATIVE_TO_SELF, 0.5f);
		rotation.setDuration(1200);
		rotation.setInterpolator(new LinearInterpolator());
		rotation.setRepeatMode(Animation.RESTART);
		rotation.setRepeatCount(Animation.INFINITE);

		Indicator.startAnimation(rotation);
	}

	public void stopIndicator() {
		Indicator.setVisibility(View.INVISIBLE);
		Indicator.setAnimation(null);
	}
.
.
.
when process ends call
stopIndicator();
```

//save this png @ drawable
[![](https://www.pipiscrew.com/wp-content/uploads/2013/12/indicator.png "indicator")](https://www.pipiscrew.com/wp-content/uploads/2013/12/indicator.png)

origin - http://www.pipiscrew.com/?p=523 android-indicator