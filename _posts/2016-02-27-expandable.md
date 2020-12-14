---
title: Expandable Listview with checkboxes
author: PipisCrew
date: 2016-02-27
categories: [android]
toc: true
---

reference - [http://www.androidhive.info/2013/07/android-expandable-list-view-tutorial/](http://www.androidhive.info/2013/07/android-expandable-list-view-tutorial/)

![Snap111](https://www.pipiscrew.com/wp-content/uploads/2016/02/Snap111.png)

```js
//@activity
    <linearlayout android:id="@+id/frag_settings_row02_categories_child" android:layout_width="fill_parent" android:layout_height="wrap_content" android:orientation="vertical" android:padding="20dp">

        <expandablelistview android:id="@+id/frag_settings_row02_categories_explstv" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_margin="5dip"></expandablelistview>
    </linearlayout>
```

```js
//@the row
<?xml version="1.0" encoding="utf-8"?>
<relativelayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="match_parent" android:layout_height="match_parent">

    <linearlayout android:layout_width="wrap_content" android:layout_height="wrap_content" android:baselinealigned="false" android:layout_marginleft="35dp" android:orientation="horizontal">

        <textview android:id="@+id/frag_settings_row_detail_02_categories_row_title" android:layout_width="wrap_content" android:layout_height="wrap_content" android:textsize="15sp"></textview>
    </linearlayout>

    <checkbox android:id="@+id/frag_settings_row_detail_02_categories_row_check" android:layout_width="wrap_content" android:layout_height="wrap_content" android:focusable="false" android:layout_alignparentright="true" android:gravity="right"></checkbox>

</relativelayout>
```

```js
CREATE TABLE [categories]
(id INTEGER,
category_name TEXT,
parent_id INTEGER);
```

```js
//fragment.java
public class Frag_Settings extends Fragment implements OnItemClickListener {

	// ////////////expandable
	private Frag_Settings_Categories_Adapter listAdapter;
	private ExpandableListView expListView;
	private List<frag_settings_categories> listHeader_Categories;
	private HashMap<frag_settings_categories,></frag_settings_categories,><frag_settings_categories>> listDataChild;
	// ////////////expandable

	@Override
	public void onActivityCreated(Bundle savedInstanceState) {
		super.onActivityCreated(savedInstanceState);

		expListView = (ExpandableListView) getActivity().findViewById(R.id.frag_settings_row02_categories_explstv);
		listHeader_Categories = new ArrayList<frag_settings_categories>();
		listDataChild = new HashMap<frag_settings_categories,></frag_settings_categories,><frag_settings_categories>>();

		listAdapter = new Frag_Settings_Categories_Adapter(getActivity(), listHeader_Categories, listDataChild);
		expListView.setAdapter(listAdapter);

		//fetch recordset by DBASE
		CategoriesDatasource categories_datasource = new CategoriesDatasource(getActivity());

		// get HEAD CATEGORY (categories - parent_id=0)
		for (Categories d : categories_datasource.getAllCategoriess()) {
			if (d.getparent_id()==0)
				listHeader_Categories.add(new Frag_Settings_Categories(d.getid(), d.getcategory_name(), false));
		}

		// get HEAD CHILD ITEMS (sub_categories - parent_id = cat_head)
		List<frag_settings_categories> child_Categories = null;
		for (Frag_Settings_Categories cat_head : listHeader_Categories) {

			// each time instantiate the list
			child_Categories = new ArrayList<frag_settings_categories>();

			// get all sub_categories has parent the cat_head
			for (Categories sub_cat : categories_datasource.getAllCategoriess()) {
				if (sub_cat.getparent_id() == cat_head.getId()) {
					child_Categories.add(new Frag_Settings_Categories(sub_cat.getid(), sub_cat.getcategory_name(), false));
				}
			}

			//for each HEAD CATEGORY - hang children
			listDataChild.put(cat_head, child_Categories);
		}
	}
```

```js
//Frag_Settings_Categories_Adapter.java
import java.util.HashMap;
import java.util.List;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseExpandableListAdapter;
import android.widget.CheckBox;
import android.widget.CompoundButton;
import android.widget.CompoundButton.OnCheckedChangeListener;
import android.widget.TextView;

public class Frag_Settings_Categories_Adapter extends BaseExpandableListAdapter {

	private List<frag_settings_categories> data;
	private HashMap<frag_settings_categories,></frag_settings_categories,><frag_settings_categories>> child;
	private Context context;

	public Frag_Settings_Categories_Adapter(Context context, List<frag_settings_categories> items, HashMap<frag_settings_categories,></frag_settings_categories,><frag_settings_categories>> listChildData) {
		this.context = context;
		this.data = items;
		this.child = listChildData;

	}

	@Override
	public Object getChild(int groupPosition, int childPosititon) {
		return this.child.get(this.data.get(groupPosition)).get(childPosititon);
	}

	@Override
	public long getChildId(int groupPosition, int childPosition) {
		return childPosition;
	}

	// //////////////////// CHILD ITEM
	@Override
	public View getChildView(int groupPosition, int childPosition, boolean isLastChild, View convertView, ViewGroup parent) {
		if (convertView == null) {
			LayoutInflater infalInflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
			convertView = infalInflater.inflate(R.layout.frag_settings_row_detail_02_categories_row, null);
		}

		ViewHolder holder;
		holder = new ViewHolder();
		holder.rowText = (TextView) convertView.findViewById(R.id.frag_settings_row_detail_02_categories_row_title);
		holder.rowChk = (CheckBox) convertView.findViewById(R.id.frag_settings_row_detail_02_categories_row_check);

		// http://stackoverflow.com/questions/12647001/listview-with-custom-adapter-containing-checkboxes
		holder.rowChk.setTag(String.valueOf(groupPosition) +  "|" + String.valueOf(childPosition)); // store the List<>position in TAG

		holder.rowChk.setOnCheckedChangeListener(new OnCheckedChangeListener() {

			public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
				String tag_txt = buttonView.getTag().toString();
				int delimiter_pos =tag_txt.indexOf("|");

				int head_id =Integer.parseInt(tag_txt.substring(0,delimiter_pos));
				int child_id = Integer.parseInt(tag_txt.substring(delimiter_pos+1));

				child.get(data.get(head_id)).get(child_id).setIs_selected(isChecked); // use of List<>position
			}

		});

		// get CHILD items (search via HEAD item)
		List<frag_settings_categories> single = child.get(data.get(groupPosition));

		// >>>>>>>>>> get - which item the view requires via childPosition
		holder.rowText.setText(single.get(childPosition).getTitle());

		if (single.get(childPosition).getIs_selected())
			holder.rowChk.setChecked(true);
		else
			holder.rowChk.setChecked(false);

		return convertView;
	}

	@Override
	public int getChildrenCount(int groupPosition) {
		return this.child.get(this.data.get(groupPosition)).size();
	}

	@Override
	public Object getGroup(int groupPosition) {
		return this.data.get(groupPosition);
	}

	@Override
	public int getGroupCount() {
		return this.data.size();
	}

	@Override
	public long getGroupId(int groupPosition) {
		return groupPosition;
	}

	// //////////////////// HEAD ITEM
	@Override
	public View getGroupView(int groupPosition, boolean isExpanded, View convertView, ViewGroup parent) {

		if (convertView == null) {
			LayoutInflater infalInflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
			convertView = infalInflater.inflate(R.layout.frag_settings_row_detail_02_categories_row, null);
		}

		ViewHolder holder;
		holder = new ViewHolder();
		holder.rowText = (TextView) convertView.findViewById(R.id.frag_settings_row_detail_02_categories_row_title);
		holder.rowChk = (CheckBox) convertView.findViewById(R.id.frag_settings_row_detail_02_categories_row_check);

		// http://stackoverflow.com/questions/12647001/listview-with-custom-adapter-containing-checkboxes
		holder.rowChk.setTag(Integer.valueOf(groupPosition)); // store the List<>position in TAG

		holder.rowChk.setOnCheckedChangeListener(new OnCheckedChangeListener() {

			public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
				data.get((Integer) buttonView.getTag()).setIs_selected(isChecked); // use of List<>position

				notifyDataSetChanged(); //refresh view
			}

		});

		holder.rowText.setText(data.get(groupPosition).getTitle());

		if (data.get(groupPosition).getIs_selected()) {
			holder.rowChk.setChecked(true);
			manipulate_children_value((groupPosition),true);
		} else {
			holder.rowChk.setChecked(false);
			manipulate_children_value(groupPosition,false);
		}

		return convertView;
	}

	private void manipulate_children_value(int head_position, Boolean val) {
//		List<frag_settings_categories> x = child.get(data.get(head_position));
//		
//		for (int i = 0; i < x.size();="" i++)="" {="" child.get(data.get(head_position)).get(i).setis_selected(val);="" }="" similar="" for="" (frag_settings_categories="" x="" :="" child.get(data.get(head_position)))="" {="" x.setis_selected(val);="" }="" }="" @override="" public="" void="" notifydatasetchanged()="" {="" super.notifydatasetchanged();="" }="" @override="" public="" boolean="" hasstableids()="" {="" http://stackoverflow.com/a/18217552/1320686="" return="" true;="" }="" @override="" public="" boolean="" ischildselectable(int="" groupposition,="" int="" childposition)="" {="" return="" true;="" }="" class="" viewholder="" {="" textview="" rowtext;="" checkbox="" rowchk;="" }="" }="" frag_settings_categories.java="" public="" class="" frag_settings_categories="" {="" private="" int="" id;="" private="" string="" title;="" private="" boolean="" is_selected;="" public="" frag_settings_categories(long="" id,string="" title,="" boolean="" is_selected){="" this.id="(int)" id;="" this.title="title;" this.is_selected="is_selected;" }="" public="" int="" getid()="" {="" return="" id;="" }="" public="" void="" setid(int="" id)="" {="" this.id="id;" }="" public="" string="" gettitle()="" {="" return="" title;="" }="" public="" void="" settitle(string="" title)="" {="" this.title="title;" }="" public="" boolean="" getis_selected()="" {="" return="" is_selected;="" }="" public="" void="" setis_selected(boolean="" is_selected)="" {="" this.is_selected="is_selected;" }="" }="" ```="" x.size();="" i++)="" {="" child.get(data.get(head_position)).get(i).setis_selected(val);="" }="" similar="" for="" (frag_settings_categories="" x="" :="" child.get(data.get(head_position)))="" {="" x.setis_selected(val);="" }="" }="" @override="" public="" void="" notifydatasetchanged()="" {="" super.notifydatasetchanged();="" }="" @override="" public="" boolean="" hasstableids()="" {="" http://stackoverflow.com/a/18217552/1320686="" return="" true;="" }="" @override="" public="" boolean="" ischildselectable(int="" groupposition,="" int="" childposition)="" {="" return="" true;="" }="" class="" viewholder="" {="" textview="" rowtext;="" checkbox="" rowchk;="" }="" }="" frag_settings_categories.java="" public="" class="" frag_settings_categories="" {="" private="" int="" id;="" private="" string="" title;="" private="" boolean="" is_selected;="" public="" frag_settings_categories(long="" id,string="" title,="" boolean="" is_selected){="" this.id="(int)" id;="" this.title="title;" this.is_selected="is_selected;" }="" public="" int="" getid()="" {="" return="" id;="" }="" public="" void="" setid(int="" id)="" {="" this.id="id;" }="" public="" string="" gettitle()="" {="" return="" title;="" }="" public="" void="" settitle(string="" title)="" {="" this.title="title;" }="" public="" boolean="" getis_selected()="" {="" return="" is_selected;="" }="" public="" void="" setis_selected(boolean="" is_selected)="" {="" this.is_selected="is_selected;" }="" }=""></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories>

origin - http://www.pipiscrew.com/?p=4037 android-expandable-listview-with-checkboxes