---
title: listview w/ checkboxes filled by sqlite
author: PipisCrew
date: 2016-02-29
categories: [android]
toc: true
---

```js
//fragment.java
public class Frag_Settings extends Fragment implements OnItemClickListener {

	// //////////// listview
	private ListView frag_settings_row03_products_lstv;
	private Frag_Settings_products_Adapter lstv_products_adapter;
	private List<products> Frag_Settings_products_LIST = null;
	// //////////// listview

@Override
public void onActivityCreated(Bundle savedInstanceState) {	
	frag_settings_row03_products_lstv = (ListView) getActivity().findViewById(R.id.frag_settings_row03_products_lstv);

	Frag_Settings_products_LIST = new ArrayList<products>();
	frag_settings_row03_products_lstv.setOnItemClickListener(this);
	lstv_products_adapter = new Frag_Settings_products_Adapter(getActivity(), Frag_Settings_products_LIST);

	productsDatasource products_datasource = new productsDatasource(getActivity()); //sqlite

	for (products d : products_datasource.getAllproducts()) { // plain select * from table
		Frag_Settings_products_LIST.add(new products(d.getID(), d.getPRODUCT_NAME(), false));
	}

	 frag_settings_row03_products_lstv.setAdapter(lstv_products_adapter);
}

//products.java
public class products {
	private int id;
	private String title;
	private Boolean is_selected;

	public products()
	{	

	}	

	public products(long id,String title, Boolean is_selected){

		this.id=(int) id;
		this.title=title;
		this.is_selected=is_selected;
	}

	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getTitle() {
		return title;
	}
	public void setTitle(String title) {
		this.title = title;
	}
	public Boolean getIs_selected() {
		return is_selected;
	}
	public void setIs_selected(Boolean is_selected) {
		this.is_selected = is_selected;
	}
}
```

```js
//Frag_Settings_products_Adapter.java
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.CheckBox;
import android.widget.CompoundButton;
import android.widget.CompoundButton.OnCheckedChangeListener;
import android.widget.TextView;

public class Frag_Settings_products_Adapter extends BaseAdapter {

	private List<products> data;
	private Context context;

	public Frag_Settings_products_Adapter(Context context,  List<products> items) {
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
		convertView = infalInflater.inflate(R.layout.frag_settings_row_detail_04_row, null);

		ViewHolder holder;
		holder = new ViewHolder();
		holder.rowText = (TextView) convertView.findViewById(R.id.frag_settings_row_detail_04_row_title);
		holder.rowChk = (CheckBox) convertView.findViewById(R.id.frag_settings_row_detail_04_row_check);

		//http://stackoverflow.com/questions/12647001/listview-with-custom-adapter-containing-checkboxes
		holder.rowChk.setTag(Integer.valueOf(position)); //store the List<>position in TAG

		holder.rowChk.setOnCheckedChangeListener(new OnCheckedChangeListener(){

            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
            	data.get((Integer)buttonView.getTag()).setIs_selected(isChecked); //use of List<>position
            }

        });

		holder.rowText.setText(data.get(position).getproduct_NAME());

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
//frag_settings_row_detail_04_row.xml
<?xml version="1.0" encoding="utf-8"?>
<relativelayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="match_parent" android:layout_height="match_parent">

    <linearlayout android:layout_width="match_parent" android:layout_height="wrap_content" android:baselinealigned="false" android:layout_marginleft="35dp" android:layout_marginright="25dp" android:orientation="horizontal">

        <textview android:id="@+id/frag_settings_row_detail_04_products_row_title" android:layout_width="wrap_content" android:layout_height="wrap_content" android:lines="2" android:textsize="15sp"></textview>
    </linearlayout>

    <checkbox android:id="@+id/frag_settings_row_detail_04_products_row_check" android:layout_width="wrap_content" android:layout_height="wrap_content" android:focusable="false" android:layout_alignparentright="true" android:gravity="right"></checkbox>

</relativelayout>
```

similar - [https://www.pipiscrew.com/2016/02/android-listview-with-custom-adapter-viewholder/](https://www.pipiscrew.com/2016/02/android-listview-with-custom-adapter-viewholder/)</products></products></products></products>

origin - http://www.pipiscrew.com/?p=4107 android-listview-w-checkboxes-filled-by-sqlite