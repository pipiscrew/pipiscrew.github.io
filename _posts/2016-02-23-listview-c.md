---
title: listview checkbox
author: PipisCrew
date: 2016-02-23
categories: [android]
toc: true
---

Implement a listview with checkboxes, store&load to sharedpreferences.

![Snap102](https://www.pipiscrew.com/wp-content/uploads/2016/02/Snap102.png)

```js
//Frag_Settings.java
public class Frag_Settings extends Fragment implements OnItemClickListener {

// ////////////listview
ListView lstv;
Frag_Settings_Categories_Adapter lstv_adapter;
List<frag_settings_categories> Frag_Settings_Categories_LIST = null;

@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
	View rootView = inflater.inflate(R.layout.frag_settings, container, false);

	return rootView;
}

@Override
public void onActivityCreated(Bundle savedInstanceState) {
	super.onActivityCreated(savedInstanceState);

	//button save - store *checked* listview row IDs to SharedPreferences
	Button btn_date = (Button) getActivity().findViewById(R.id.frag_settings_btn_save);

	btn_date.setOnClickListener(new View.OnClickListener() {
		@Override
		public void onClick(View v) {
			Set<string> set = new HashSet<string>();

			for (Frag_Settings_Categories item : Frag_Settings_Categories_LIST) {
				if (item.getIs_selected())
					set.add(String.valueOf(item.getId()));
			}

			SharedPreferences.Editor prefs = General.get_pref(getActivity()).edit(); 	
			prefs.putStringSet("user_categories", set);
			prefs.commit();
		}
	});

	//connect design listview to code
	lstv = (ListView) getActivity().findViewById(R.id.frag_settings_row02_categories_lstv);
	Frag_Settings_Categories_LIST = new ArrayList<frag_settings_categories>();
	lstv.setOnItemClickListener(this);
	lstv_adapter = new Frag_Settings_Categories_Adapter(getActivity(), Frag_Settings_Categories_LIST);
	lstv.setAdapter(lstv_adapter);

	//fill listview by dbase records
	CategoriesDatasource categories_datasource = new CategoriesDatasource(getActivity());

	for (Categories d : categories_datasource.getAllCategoriess()) {
		Frag_Settings_Categories_LIST.add(new Frag_Settings_Categories(d.getid(),d.getcategory_name(),false));
	}

	lstv.setAdapter(lstv_adapter);

	//load user prefs - retrieve *checked* listview row IDs
	SharedPreferences prefs=  General.get_pref(getActivity());
	Set<string> user_categories_set = prefs.getStringSet("user_categories", null);

	if (user_categories_set!=null)
	{
		List<string> user_categories = new ArrayList<string>(user_categories_set);

		for(int i = 0 ; i < user_categories.size()="" ;="" i++){="" for="" (frag_settings_categories="" item="" :="" frag_settings_categories_list)="" {="" if="" (user_categories.get(i).equals(string.valueof(item.getid())))="" item.setis_selected(true);="" }="" }="" notify="" view="" lstv_adapter.notifydatasetchanged();="" }="" }="" ```=""  =""  ="" ```js="" frag_settings_categories.java="" public="" class="" frag_settings_categories="" {="" private="" int="" id;="" private="" string="" title;="" private="" boolean="" is_selected;="" public="" frag_settings_categories(long="" id,string="" title,="" boolean="" is_selected){="" this.id="(int)" id;="" this.title="title;" this.is_selected="is_selected;" }="" public="" int="" getid()="" {="" return="" id;="" }="" public="" void="" setid(int="" id)="" {="" this.id="id;" }="" public="" string="" gettitle()="" {="" return="" title;="" }="" public="" void="" settitle(string="" title)="" {="" this.title="title;" }="" public="" boolean="" getis_selected()="" {="" return="" is_selected;="" }="" public="" void="" setis_selected(boolean="" is_selected)="" {="" this.is_selected="is_selected;" }="" }="" ```=""  =""  ="" ```js="" frag_settings_categories_adapter.java="" import="" java.util.list;="" import="" android.content.context;="" import="" android.view.layoutinflater;="" import="" android.view.view;="" import="" android.view.viewgroup;="" import="" android.widget.baseadapter;="" import="" android.widget.checkbox;="" import="" android.widget.compoundbutton;="" import="" android.widget.compoundbutton.oncheckedchangelistener;="" import="" android.widget.textview;="" public="" class="" frag_settings_categories_adapter="" extends="" baseadapter="" {="" private=""><frag_settings_categories> data;
	private Context context;

	public Frag_Settings_Categories_Adapter(Context context,  List<frag_settings_categories> items) {
		this.context =context;
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
		convertView = infalInflater.inflate(R.layout.frag_settings_row_detail_02_categories_row, null);

		ViewHolder holder;
		holder = new ViewHolder();
		holder.rowText = (TextView) convertView.findViewById(R.id.frag_settings_row_detail_02_categories_row_title);
		holder.rowChk = (CheckBox) convertView.findViewById(R.id.frag_settings_row_detail_02_categories_row_check);

		//http://stackoverflow.com/questions/12647001/listview-with-custom-adapter-containing-checkboxes
		holder.rowChk.setTag(Integer.valueOf(position)); //store the List<>position in TAG

		holder.rowChk.setOnCheckedChangeListener(new OnCheckedChangeListener(){

            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
            	data.get((Integer)buttonView.getTag()).setIs_selected(isChecked); //use of List<>position
            }

        });

		holder.rowText.setText(data.get(position).getTitle());

		if (data.get(position).getIs_selected())
			holder.rowChk.setChecked(true);
		else 
			holder.rowChk.setChecked(false);

		return convertView;
	}

	class ViewHolder {
		TextView rowText;
		CheckBox rowChk;
	}

}
```

```js
//frag_settings.xml
<?xml version="1.0" encoding="utf-8"?>
<linearlayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="fill_parent" android:layout_height="fill_parent" android:background="#f4f4f4" android:orientation="vertical">

	<listview android:id="@+id/frag_settings_row02_categories_lstv" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_margin="5dip"></listview>

	<button android:id="@+id/frag_settings_btn_save" style="@style/ButtonText" android:layout_width="wrap_content" android:layout_margintop="10dp" android:background="@drawable/btn_red" android:layout_gravity="center_horizontal" android:paddingleft="8dp" android:paddingright="8dp" android:text="save">
	</button>

</linearlayout>
```

```js
//frag_settings_row_detail_02_categories_row.xml
<?xml version="1.0" encoding="utf-8"?>
<relativelayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="match_parent" android:layout_height="match_parent">

    <linearlayout android:layout_width="wrap_content" android:layout_height="wrap_content" android:baselinealigned="false" android:layout_marginleft="5dp" android:orientation="horizontal">

        <textview android:id="@+id/frag_settings_row_detail_02_categories_row_title" android:layout_width="wrap_content" android:layout_height="wrap_content" android:textsize="15sp"></textview>
    </linearlayout>

    <checkbox android:id="@+id/frag_settings_row_detail_02_categories_row_check" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_alignparentright="true" android:gravity="right"></checkbox>

</relativelayout>
```</frag_settings_categories></frag_settings_categories></string></string></string></frag_settings_categories></string></string></frag_settings_categories>

origin - http://www.pipiscrew.com/?p=3980 android-listview-checkbox