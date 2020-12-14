---
title: dont carry two images for collapse
author: PipisCrew
date: 2016-02-22
categories: [android]
toc: true
---

```js
//res/anim/ic_arrow_collapse.xml
<?xml version="1.0" encoding="utf-8"?>
<rotate xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/ic_arrow_expand"
    android:fromDegrees="180"
    android:pivotX="50%"
    android:pivotY="50%"
    android:toDegrees="180" />
```

```js
//activity
        <ImageView
            android:id="@+id/img_toggler"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_marginRight="10dp"
            android:background="@drawable/ic_arrow_expand" />
```

```js
//code
	Animation rotateAnimation = AnimationUtils.loadAnimation(getActivity(), R.anim.ic_arrow_collapse);
	ImageView  imng = (ImageView) getActivity().findViewById(R.id.img_toggler);
	imng.startAnimation(rotateAnimation);
```

origin - http://www.pipiscrew.com/?p=3947 android-dont-carry-two-images-for-collapse