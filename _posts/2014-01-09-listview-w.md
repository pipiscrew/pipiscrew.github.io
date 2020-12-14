---
title: listview with image + checkbox
author: PipisCrew
date: 2014-01-09
categories: []
toc: true
---

```js
//xml
            <listview android:id="@+id/lstvTESTSCATEGORIES" android:layout_width="wrap_content" android:layout_height="200dp" android:layout_below="@id/tableRow5_USERPROFILE" android:layout_margin="5dip"></listview>

//xml for row
			<?xml version="1.0" encoding="utf-8"?>
			<relativelayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="match_parent" android:layout_height="match_parent">

			    <linearlayout android:layout_width="wrap_content" android:layout_height="wrap_content" android:baselinealigned="false" android:layout_marginleft="5dp" android:orientation="horizontal">

			        <imageview android:id="@+id/IMG_userProfile_TESTROW" android:layout_width="40dp" android:layout_height="40dp" android:layout_marginright="5dp" android:scaletype="fitStart"></imageview>

			        <textview android:id="@+id/rowTitle_TESTROW" android:layout_width="wrap_content" android:layout_height="wrap_content" android:textsize="15sp"></textview>
			    </linearlayout>

			    <checkbox android:id="@+id/chk_TESTROW" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_alignparentright="true" android:gravity="right"></checkbox>

			</relativelayout>
```

//the class
```js
			public class Generic4lstv {
				public String imgURL;
				public String rowText;
				public String rowID;
				public Boolean isSelected;

				public String getRowID() {
					return rowID;
				}

				public void setRowID(String rowID) {
					this.rowID = rowID;
				}

				public String getImgURL() {
					return imgURL;
				}

				public void setImgURL(String imgURL) {
					this.imgURL = imgURL;
				}

				public String getRowText() {
					return rowText;
				}

				public void setRowText(String rowText) {
					this.rowText = rowText;
				}

				public Boolean getIsSelected() {
					return isSelected;
				}

				public void setIsSelected(Boolean isSelected) {
					this.isSelected = isSelected;
				}
			}

```

//java activity
```js
			// Public declaration
			ListView lstv;
			User_Profile_TESTCatsAdapter listAdapter;
			List<generic4lstv> rowItems = new ArrayList<generic4lstv>();

			protected void onCreate(Bundle savedInstanceState) {			
				lstv = (ListView) findViewById(R.id.lstvTESTSCATEGORIES);
				lstv.setOnItemClickListener(this);
				listAdapter = new User_Profile_TESTCatsAdapter(this, rowItems);
				lstv.setAdapter(listAdapter);

				fillLSTV;
			}

			private void fillLSTV() {
				Generic4lstv rowItem;

				for (DataSnapshot child : snapshot.getChildren()) {
					rowItem = new Generic4lstv();

					String title = child.child("title").getValue().toString().trim();

					rowItem.setImgURL("to be fixed");
					rowItem.setRowText(title);
					rowItem.setRowID(child.getName());

//TESTCAT holds the saved checked rows
//in current example the load is not implemented!
				//	if (TESTCAT.indexOf(child.getName())>-1)
				//		rowItem.setIsSelected(true);
				//	else 
				//		rowItem.setIsSelected(false);

					rowItems.add(rowItem);

				}

				listAdapter.notifyDataSetChanged();
			}

			@Override
			public void onBackPressed() {
				//save on back!
				String CompCategories="#";

				for(Generic4lstv item : rowItems ){
					if (item.getIsSelected())
						CompCategories+= item.getRowID() + "#";
				}

				SharedPreferences options = getSharedPreferences("userprofile", MODE_PRIVATE);
				SharedPreferences.Editor editor = options.edit();
				editor.putString("CompCategories", CompCategories);
				editor.commit();

				super.onBackPressed();
			}
```

//java listview adapter
```js

			import java.util.List;

			import android.app.Activity;
			import android.content.Context;
			import android.util.DisplayMetrics;
			import android.view.LayoutInflater;
			import android.view.View;
			import android.view.ViewGroup;
			import android.widget.BaseAdapter;
			import android.widget.CheckBox;
			import android.widget.CompoundButton;
			import android.widget.CompoundButton.OnCheckedChangeListener;
			import android.widget.ImageView;
			import android.widget.TextView;

			import com.squareup.picasso.Picasso;

			public class User_Profile_TESTCatsAdapter extends BaseAdapter {

				private List<generic4lstv> data;
				private Activity context;

				public User_Profile_TESTCatsAdapter(Activity a, List<generic4lstv> items) {
					this.context = a;
					this.data = items;
				}

				@Override
				public int getCount() {
					return data.size();
				}

				@Override
				public Object getItem(int position) {
					return data.get(position);
				}

				@Override
				public long getItemId(int position) {
					return position;
				}

				@Override
				public View getView(int position, View convertView, ViewGroup arg2) {
					LayoutInflater infalInflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
					convertView = infalInflater.inflate(R.layout.activity_user_profile_TEST_categ_row, null);

					ViewHolder holder;
					holder = new ViewHolder();
					holder.rowText = (TextView) convertView.findViewById(R.id.rowTitle_TESTROW);
					holder.rowImage = (ImageView) convertView.findViewById(R.id.IMG_userProfile_TESTROW);
					holder.rowChk = (CheckBox) convertView.findViewById(R.id.chk_TESTROW);

					//http://stackoverflow.com/questions/12647001/listview-with-custom-adapter-containing-checkboxes
					holder.rowChk.setTag(Integer.valueOf(position)); //store the List<>position in TAG

					holder.rowChk.setOnCheckedChangeListener(new OnCheckedChangeListener(){

			            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
			            	data.get((Integer)buttonView.getTag()).setIsSelected(isChecked); //use of List<>position
			            }

			        });

					holder.rowText.setText(data.get(position).getRowText());

					if (data.get(position).getIsSelected())
						holder.rowChk.setChecked(true);
					else 
						holder.rowChk.setChecked(false);

					Picasso.with(context).load(picName).into(holder.rowImage);

					return convertView;
				}

				class ViewHolder {
					ImageView rowImage;
					TextView rowText;
					CheckBox rowChk;
				}
			}

```
![](https://www.pipiscrew.com/wp-content/uploads/2014/01/Snap431.png "Snap431")</generic4lstv></generic4lstv></generic4lstv></generic4lstv>

origin - http://www.pipiscrew.com/?p=635 android-listview-with-image-checkbox