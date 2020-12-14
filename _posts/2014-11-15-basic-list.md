---
title: Basic Listview Adapter
author: PipisCrew
date: 2014-11-15
categories: []
toc: true
---

```js

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity" >

    <ListView
        android:id="@+id/lstv"
        android:layout_width="fill_parent"
        android:layout_height="match_parent"
        android:layout_margin="5dp"/>
</RelativeLayout>

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >

        <TextView
            android:id="@+id/txt_name"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textSize="20sp" />

        <TextView
            android:id="@+id/txt_plate"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textSize="12sp" />
</LinearLayout>
```

MainActivity.java
```js
import java.util.ArrayList;
import java.util.List;

import android.app.Activity;
import android.os.Bundle;
import android.view.Menu;
import android.view.View;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemClickListener;
import android.widget.ListView;
import android.widget.Toast;

public class MainActivity extends Activity implements OnItemClickListener {

	// lstv
	private ListView lstv;
	private MainActivityAdapter listAdapter;
	private List<MainActivityRow> rowItems = null;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);

		// lstv
		rowItems = new ArrayList<MainActivityRow>();
		lstv = (ListView) findViewById(R.id.lstv);
		lstv.setOnItemClickListener(this);
		listAdapter = new MainActivityAdapter(this, rowItems);

		rowItems.add(new MainActivityRow(1,"test1", "subtitle1"));
		rowItems.add(new MainActivityRow(2,"test2", "subtitle2"));
		rowItems.add(new MainActivityRow(3,"test3", "subtitle3"));
		lstv.setAdapter(listAdapter);

	}

	@Override
	public void onItemClick(AdapterView<?> arg0, View arg1, int arg2, long arg3) {
		//show clicked
		Toast.makeText(MainActivity.this, rowItems.get(arg2).getId().toString(),	Toast.LENGTH_SHORT).show();

		//add new items
		rowItems.add(new MainActivityRow(4,"test1", "subtitle1"));
		rowItems.add(new MainActivityRow(5,"test2", "subtitle2"));
		rowItems.add(new MainActivityRow(6,"test3", "subtitle3"));

		//show new items
		listAdapter.notifyDataSetChanged();
	}

}
```

MainActivityAdapter.java
```js
import java.util.List;

import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.TextView;

public class MainActivityAdapter extends BaseAdapter {

	private List<MainActivityRow> data;
	private LayoutInflater mLayoutInflater;
	private Context c; //later we will use it to getapplicationcontext

	public MainActivityAdapter(Context context, List<MainActivityRow> items) {
		this.data = items;
		this.c = context;

		mLayoutInflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
	}

	@Override
	public int getCount() {
		// getCount() represents how many items are in the ArrayList
		return data.size();
	}

	@Override
	public Object getItem(int position) {
		// get the data of an item from a specific position
		// it represents the position of the item in the ArrayList
		return data.get(position);
	}

	@Override
	public long getItemId(int position) {
		// get the position id of the item from the ArrayList
		return position;
	}

	@Override
	public View getView(int position, View convertView, ViewGroup arg2) {
		convertView = mLayoutInflater.inflate(R.layout.activity_main_row, null);

		MainActivityRow item = (MainActivityRow) getItem(position);

		((TextView) convertView.findViewById(R.id.txt_name)).setText(item.getLstv_text());
		((TextView) convertView.findViewById(R.id.txt_plate)).setText(item.getLstv_subtitle());

		// this method must return the view corresponding to the data at the specified position.
		return convertView;
	}

}
```

MainActivityRow.java
```js
public class MainActivityRow {

	private Integer id;
	private String lstv_text;
	private String lstv_subtitle;

	public MainActivityRow(Integer id, String text, String subtitle)
	{
		this.id = id;
		lstv_text=text;
		lstv_subtitle = subtitle;
	}

	public Integer getId() {
		return id;
	}

	public void setId(Integer id) {
		this.id = id;
	}

	public String getLstv_text() {
		return lstv_text;
	}
	public void setLstv_text(String lstv_text) {
		this.lstv_text = lstv_text;
	}
	public String getLstv_subtitle() {
		return lstv_subtitle;
	}
	public void setLstv_subtitle(String lstv_subtitle) {
		this.lstv_subtitle = lstv_subtitle;
	}
}

```

origin - http://www.pipiscrew.com/?p=1891 android-basic-listview-adapter