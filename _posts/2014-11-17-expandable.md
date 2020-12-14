---
title: Expandable Listview
author: PipisCrew
date: 2014-11-17
categories: []
toc: true
---

reference
[http://theopentutorials.com/tutorials/android/listview/android-expandable-list-view-example/](http://theopentutorials.com/tutorials/android/listview/android-expandable-list-view-example/)

```js
//activity_auto_moto_details.xml
<relativelayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent" android:layout_height="match_parent" tools:context=".MainActivity">

    <expandablelistview android:id="@android:id/list" android:layout_width="match_parent" android:layout_height="fill_parent">
    </expandablelistview>

</relativelayout>

//activity_auto_moto_details_row_head.xml
<?xml version="1.0" encoding="utf-8"?>
<linearlayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="match_parent" android:layout_height="match_parent" android:orientation="vertical" android:padding="10dp">

    <textview android:id="@+id/row_head" android:layout_width="wrap_content" android:layout_height="wrap_content" android:paddingleft="25dp"></textview>
</linearlayout>

//activity_auto_moto_details_row_head_child.xml
<?xml version="1.0" encoding="utf-8"?>
<relativelayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="fill_parent" android:layout_height="wrap_content" android:padding="10dp">

    <textview android:id="@+id/row_item_head" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_alignparentleft="true" android:layout_centervertical="true" android:paddingleft="25dp"></textview>

    <imageview android:id="@+id/row_item_delete" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_alignparentright="true" android:src="@drawable/delete" android:contentdescription="@string/app_name"></imageview>

</relativelayout>
```

> activity.java

```js
import java.util.ArrayList;
import java.util.LinkedHashMap;
import java.util.List;
import java.util.Map;

import android.app.ExpandableListActivity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.ExpandableListAdapter;
import android.widget.ExpandableListView;
import android.widget.ExpandableListView.OnChildClickListener;
import android.widget.Toast;

public class AutoMotoDetails extends ExpandableListActivity implements OnChildClickListener {

	List<string> groupList;
	List<string> childList;
	Map<string,></string,><string>> head;
	ExpandableListView expListView;
	AutoMotoDetailsAdapter expListAdapter;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_auto_moto_details);

		createGroupList();
		createCollection();

		expListView = getExpandableListView();

		expListAdapter = new AutoMotoDetailsAdapter(this, groupList, head);
		expListView.setAdapter(expListAdapter);

		getActionBar().setDisplayHomeAsUpEnabled(true);
	}

	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
		// Inflate the menu; this adds items to the action bar if it is present.
		getMenuInflater().inflate(R.menu.auto_moto_details, menu);
		return true;
	}

	@Override
	public boolean onOptionsItemSelected(MenuItem item) {
		switch (item.getItemId()) {
		case android.R.id.home:
			finish();
			return true;
		default:
			return super.onOptionsItemSelected(item);
		}
	}

	@Override
	public boolean onChildClick(ExpandableListView parent, View v, int groupPosition, int childPosition, long id) {
		final String selected = (String) expListAdapter.getChild(groupPosition, childPosition);
		Toast.makeText(getBaseContext(), selected, Toast.LENGTH_LONG).show();

		return true;
	}

	private void createGroupList() {
		groupList = new ArrayList<string>();
		groupList.add("HP");
		groupList.add("Dell");
		groupList.add("Lenovo");
		groupList.add("Sony");
		groupList.add("HCL");
		groupList.add("Samsung");
	}

	private void createCollection() {
		String[] hpModels = { "HP Pavilion G6-2014TX", "ProBook HP 4540", "HP Envy 4-1025TX" };
		String[] hclModels = { "HCL S2101", "HCL L2102", "HCL V2002" };
		String[] lenovoModels = { "IdeaPad Z Series", "Essential G Series", "ThinkPad X Series", "Ideapad Z Series" };
		String[] sonyModels = { "VAIO E Series", "VAIO Z Series", "VAIO S Series", "VAIO YB Series" };
		String[] dellModels = { "Inspiron", "Vostro", "XPS" };
		String[] samsungModels = { "NP Series", "Series 5", "SF Series" };

		head = new LinkedHashMap<string,></string,><string>>();

		for (String laptop : groupList) {
			if (laptop.equals("HP")) {
				loadChild(hpModels);
			} else if (laptop.equals("Dell"))
				loadChild(dellModels);
			else if (laptop.equals("Sony"))
				loadChild(sonyModels);
			else if (laptop.equals("HCL"))
				loadChild(hclModels);
			else if (laptop.equals("Samsung"))
				loadChild(samsungModels);
			else
				loadChild(lenovoModels);

			head.put(laptop, childList);
		}
	}

	private void loadChild(String[] laptopModels) {
		childList = new ArrayList<string>();
		for (String model : laptopModels)
			childList.add(model);
	}

}
```

> AutoMotoDetailsAdapter.java

```js
import java.util.List;
import java.util.Map;

import android.app.Activity;
import android.app.AlertDialog;
import android.content.Context;
import android.content.DialogInterface;
import android.graphics.Typeface;
import android.view.LayoutInflater;
import android.view.View;
import android.view.View.OnClickListener;
import android.view.ViewGroup;
import android.widget.BaseExpandableListAdapter;
import android.widget.ImageView;
import android.widget.TextView;

public class AutoMotoDetailsAdapter extends BaseExpandableListAdapter {

	private Activity context;
	private Map<string,></string,><string>> head;
	private List<string> rows;
	private LayoutInflater mLayoutInflater;

	public AutoMotoDetailsAdapter(Activity context, List<string> rows, Map<string,></string,><string>> head) {
		this.context = context;
		this.rows = rows;
		this.head = head;

		mLayoutInflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
	}

	public Object getChild(int groupPosition, int childPosition) {
		return head.get(rows.get(groupPosition)).get(childPosition);
	}

	public long getChildId(int groupPosition, int childPosition) {
		return childPosition;
	}

	public View getChildView(final int groupPosition, final int childPosition, boolean isLastChild, View convertView, ViewGroup parent) {
		convertView = mLayoutInflater.inflate(R.layout.activity_auto_moto_details_row_head_child, null);

		String item = (String) getChild(groupPosition, childPosition);

		TextView txt_row_item = (TextView) convertView.findViewById(R.id.row_item_head);

		ImageView delete = (ImageView) convertView.findViewById(R.id.row_item_delete);
		delete.setOnClickListener(new OnClickListener() {

			public void onClick(View v) {
				AlertDialog.Builder builder = new AlertDialog.Builder(context);
				builder.setMessage("Do you want to remove ?");
				builder.setCancelable(false);
				builder.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
					public void onClick(DialogInterface dialog, int id) {
						List<string> child = head.get(rows.get(groupPosition));
						child.remove(childPosition);
						notifyDataSetChanged();
					}
				});
				builder.setNegativeButton("No", new DialogInterface.OnClickListener() {
					public void onClick(DialogInterface dialog, int id) {
						dialog.cancel();
					}
				});
				AlertDialog alertDialog = builder.create();
				alertDialog.show();
			}
		});

		txt_row_item.setText(item);
		return convertView;
	}

	public int getChildrenCount(int groupPosition) {
		return head.get(rows.get(groupPosition)).size();
	}

	public Object getGroup(int groupPosition) {
		return rows.get(groupPosition);
	}

	public int getGroupCount() {
		return rows.size();
	}

	public long getGroupId(int groupPosition) {
		return groupPosition;
	}

	public View getGroupView(int groupPosition, boolean isExpanded, View convertView, ViewGroup parent) {
		String head_text = (String) getGroup(groupPosition);

		convertView = mLayoutInflater.inflate(R.layout.activity_auto_moto_details_row_head, null);

		TextView item = (TextView) convertView.findViewById(R.id.row_head);
		item.setTypeface(null, Typeface.BOLD);
		item.setText(head_text);

		return convertView;
	}

	@Override
	public boolean hasStableIds() {
		// It's used when you change the data of the Adapter, everytime you change the data the ExpandableListView should update it's views to reflect the changes.
		// if true the ExpandableListView can reuse the same View if the ID is the same.
		return true;
	}

	@Override
	public boolean isChildSelectable(int arg0, int arg1) {
		// whether the child at the specified position is selectable
		return true;
	}
}
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/11/Snap238.png "Snap238")</string></string></string></string></string></string></string></string></string></string></string>

origin - http://www.pipiscrew.com/?p=1917 android-expandable-listview