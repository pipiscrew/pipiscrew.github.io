---
title: Simple CheckBox List
author: PipisCrew
date: 2016-03-01
categories: [android]
toc: true
---

source - [http://tonyc9000.blogspot.com/2012/06/android-simple-checkbox-list.html](http://tonyc9000.blogspot.com/2012/06/android-simple-checkbox-list.html)
```js```
//string.xml
<?xml version="1.0" encoding="utf-8"?>
<resources>

    <string name="app_name">Dynamic Checkbox Array</string>

    <string-array name="data_array">
        <item>Apple</item>
        <item>Orange</item>
        <item>Lemon</item>
        <item>Lime</item>
        <item>Cherry</item>
        <item>Grape</item>
        <item>Banana</item>
        <item>Strawberry</item>
        <item>Pear</item>
        <item>Plum</item>
        <item>Apricot</item>
        <item>Pineapple</item>
        <item>Mango</item>
        <item>Coconut</item>
    </string-array>

</resources>
```js```

```js
//main.xml
<?xml version="1.0" encoding="utf-8"?>
<linearlayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="fill_parent" android:layout_height="fill_parent" android:orientation="vertical">

    <button android:id="@+id/button1" android:layout_width="match_parent" android:layout_height="wrap_content" android:onclick="button_click" android:text="Get Checked Items"></button>

    <scrollview android:id="@+id/scrollView1" android:layout_width="match_parent" android:layout_height="wrap_content">

        <linearlayout android:id="@+id/Checkbox_Layout" android:layout_width="match_parent" android:layout_height="match_parent" android:orientation="vertical">
        </linearlayout>
    </scrollview>

</linearlayout>
```

```js
//main.java
private LinearLayout checkboxLayout;
    private String[] data;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);

        checkboxLayout = (LinearLayout) findViewById(R.id.Checkbox_Layout);
        data = getResources().getStringArray(R.array.data_array);

        for (int i = 0; i < data.length;="" i++)="" {="" checkbox="" cb="new" checkbox(getapplicationcontext());="" cb.settext(data[i]);="" checkboxlayout.addview(cb);="" }="" }="" public="" void="" button_click(view="" view)="" {="" for="" (int="" i="0;" i="">< checkboxlayout.getchildcount(); i++) {
            if (checkboxlayout.getchildat(i) instanceof checkbox) {
                checkbox cb = (checkbox) checkboxlayout.getchildat(i);
                if (cb.ischecked()) {
                    toast.maketext(getapplicationcontext(),
                            cb.gettext().tostring(), toast.length_short).show();
                }
            }
        }
``` checkboxlayout.getchildcount();="" i++)="" {="" if="" (checkboxlayout.getchildat(i)="" instanceof="" checkbox)="" {="" checkbox="" cb="(CheckBox)" checkboxlayout.getchildat(i);="" if="" (cb.ischecked())="" {="" toast.maketext(getapplicationcontext(),="" cb.gettext().tostring(),="" toast.length_short).show();="" }="" }="" }=""></ checkboxlayout.getchildcount(); i++) {
            if (checkboxlayout.getchildat(i) instanceof checkbox) {
                checkbox cb = (checkbox) checkboxlayout.getchildat(i);
                if (cb.ischecked()) {
                    toast.maketext(getapplicationcontext(),
                            cb.gettext().tostring(), toast.length_short).show();
                }
            }
        }
```>

origin - http://www.pipiscrew.com/?p=4145 android-simple-checkbox-list