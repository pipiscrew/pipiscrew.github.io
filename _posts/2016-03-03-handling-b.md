---
title: Handling back button press Inside Fragments
author: PipisCrew
date: 2016-03-03
categories: [android]
toc: true
---

[http://vinsol.com/blog/2014/10/01/handling-back-button-press-inside-fragments/](http://vinsol.com/blog/2014/10/01/handling-back-button-press-inside-fragments/)

[https://github.com/Infernus666/FragmentOrientedApplication](https://github.com/Infernus666/FragmentOrientedApplication)

## minimal

```js
//on fragment itself call :
getFragmentManager().popBackStack();
```

## or handle the click on parent (aka activity)

```js
//handle click on activity shows the fragment
	@Override
	public void onBackPressed() {
		int count = getFragmentManager().getBackStackEntryCount();
		if (count == 0) { //when use it with drawer make it 1
			super.onBackPressed();
		} else {
			getFragmentManager().popBackStack();
		}
	}

//warning the beginTransaction, should be use addToBackStack
//source - http://www.tech.theplayhub.com/how_to_implement_onbackpressed_in_android_fragments/
FragmentManager fragmentManager = getFragmentManager();
fragmentManager.beginTransaction().replace(R.id.frame_container, fragment).addToBackStack(null).commit();
```

## Codepath - Creating and Using Fragments

[https://guides.codepath.com/android/Creating-and-Using-Fragments#managing-fragment-backstack](https://guides.codepath.com/android/Creating-and-Using-Fragments#managing-fragment-backstack)

## Providing Proper Back Navigation

[http://developer.android.com/training/implementing-navigation/temporal.html](http://developer.android.com/training/implementing-navigation/temporal.html)

## Handle Back Button Event in Fragment andorid – ViewPager Android 

[http://www.quicktips.in/how-to-handle-back-button-event-in-fragment-andorid-viewpager-android-tutorial/](http://www.quicktips.in/how-to-handle-back-button-event-in-fragment-andorid-viewpager-android-tutorial/)

origin - http://www.pipiscrew.com/?p=4028 android-handling-back-button-press-inside-fragments