---
title: listview filled by response of a POST made to webservice - with custom adapter + viewholder
author: PipisCrew
date: 2016-02-29
categories: [android]
toc: true
---

//reference - [http://loopj.com/android-async-http/](http://loopj.com/android-async-http/)

```js
//fragment.java
private ListView lstv;
private Frag_Products_Adapter lstv_adapter;
private List<frag_product> Frag_Product_LIST = null;

@Override
public void onActivityCreated(Bundle savedInstanceState) {
	super.onActivityCreated(savedInstanceState);

	// init list
	Frag_Product_LIST = new ArrayList<frag_product>();

	lstv = (ListView) getView().findViewById(R.id.frag_lstv);
	lstv.setOnItemClickListener(this);
	lstv_adapter = new Frag_Products_Adapter(getActivity(), Frag_Product_LIST);
	lstv.setAdapter(lstv_adapter);

	// EndlessScrollListener
	lstv.setOnScrollListener(new EndlessScrollListener());

	get_products();
}

private void get_products() {
	AsyncHttpClient client = new AsyncHttpClient();
	RequestParams clparam = new RequestParams();

	clparam.add("x", Dynomite.aid);

	client.post(getActivity(), "http://www.x.com/mobile.ashx", clparam, new AsyncHttpResponseHandler() {

		@Override
		public void onFailure(Throwable t, String error){
			General.mes(getActivity(), "Error1 : " + error);				
		}

		@Override
		public void onSuccess(String response) {
			if (response == null || response.length() < 10)="" return;="" string="" resp="response;" jsonarray="" products="null;" frag_product="" item="null;" try="" {="" products="new" jsonarray(resp);="" if="" (products="=" null="" ||="" resp.length()="">< 10)="" return;="" jsonobject="" product;="" for="" (int="" i="0;" i="">< products.length();="" i++)="" {="" item="new" frag_product();="" product="(JSONObject)" products.get(i);="" item.setid(product.getint("id"));="" item.setdescription(product.getstring("description"));="" if="" (product.isnull("subcategory_id"))="" item.setsubcategory_id(0);="" else="" item.setsubcategory_id(product.getint("subcategory_id"));="" frag_product_list.add(item);="" }="" }="" catch="" (jsonexception="" e)="" {="" general.mes(getactivity(),="" "error2="" :="" "="" +="" e.getmessage());="" }="" finally="" {="" lstv_adapter.notifydatasetchanged();="" progress.dismiss();="" }="" }="" });="" }="" public="" class="" endlessscrolllistener="" implements="" onscrolllistener="" {="" private="" int="" visiblethreshold="5;" private="" int="" currentpage="0;" private="" int="" previoustotal="0;" private="" boolean="" loading="true;" public="" endlessscrolllistener()="" {="" }="" public="" endlessscrolllistener(int="" visiblethreshold)="" {="" this.visiblethreshold="visibleThreshold;" }="" @override="" public="" void="" onscroll(abslistview="" view,="" int="" firstvisibleitem,="" int="" visibleitemcount,="" int="" totalitemcount)="" {="" if="" (loading)="" {="" if="" (totalitemcount=""> previousTotal) {
				loading = false;
				previousTotal = totalItemCount;
				currentPage++;
			}
		}
		if (!loading && (totalItemCount - visibleItemCount) <= (firstvisibleitem="" +="" visiblethreshold))="" {="" i="" load="" the="" next="" page="" of="" gigs="" using="" a="" background="" task,="" but="" you="" can="" call="" any="" function="" here.="" new="" loadgigstask().execute(currentpage="" +="" 1);="" loading="true;" }="" }="" @override="" public="" void="" onscrollstatechanged(abslistview="" view,="" int="" scrollstate)="" {="" }="" }="" frag_product.java="" public="" class="" frag_product="" {="" private="" int="" id;="" private="" string="" description;="" private="" int="" subcategory_id;="" public="" string="" getdescription()="" {="" return="" description;="" }="" public="" void="" setdescription(string="" description)="" {="" this.description="description;" }="" public="" int="" getid()="" {="" return="" id;="" }="" public="" void="" setid(int="" id)="" {="" this.id="id;" }="" public="" int="" getsubcategory_id()="" {="" return="" subcategory_id;="" }="" public="" void="" setsubcategory_id(int="" subcategory_id)="" {="" this.subcategory_id="subcategory_id;" }="" }="" ```=""  =""  ="" ```js="" frag_products_adapter.java="" import="" java.util.list;="" import="" android.app.activity;="" import="" android.content.context;="" import="" android.graphics.paint;="" import="" android.util.log;="" import="" android.view.layoutinflater;="" import="" android.view.view;="" import="" android.view.viewgroup;="" import="" android.widget.baseadapter;="" import="" android.widget.imageview;="" import="" android.widget.linearlayout;="" import="" android.widget.textview;="" import="" com.squareup.picasso.picasso;="" public="" class="" frag_products_adapter="" extends="" baseadapter="" {="" context="" context;=""></=><frag_product> rowItem;

	Frag_Products_Adapter(Context context, List<frag_product> rowItem) {
		this.context = context;
		this.rowItem = rowItem;

	}

	@Override
	public int getCount() {

		return rowItem.size();
	}

	@Override
	public Object getItem(int position) {

		return rowItem.get(position);
	}

	@Override
	public long getItemId(int position) {

		return rowItem.indexOf(getItem(position));
	}

	@Override
	public View getView(int position, View convertView, ViewGroup parent) {

		if (convertView == null) {
			LayoutInflater mInflater = (LayoutInflater) context.getSystemService(Activity.LAYOUT_INFLATER_SERVICE);
			convertView = mInflater.inflate(R.layout.frag_lstv_item, null);
		}

		ViewHolder holder;
		holder = new ViewHolder();

		holder.product_image = (ImageView) convertView.findViewById(R.id.frag__product_image);
		holder.product_description = (TextView) convertView.findViewById(R.id.frag__product_description);

		Frag_Product item = rowItem.get(position);

		Picasso.with(context).load("http://images.x.com/" + item.getImage_url()).into(holder.product_image);

		// sub-category - views are recycled - http://stackoverflow.com/a/6118581/1320686
		if (item.getSubcategory_id() > 0) {
			holder.product_sub_category.setText(item.getSubcategory_name());
			holder.product_sub_category.setVisibility(View.VISIBLE);
		} else {
			holder.product_sub_category.setVisibility(View.GONE);
		}

		return convertView;
	}

	class ViewHolder {
		// product
		ImageView product_image;
		TextView product_description;
		TextView product_sub_category;
	}
}

```

[https://www.pipiscrew.com/2016/02/android-listview-w-checkboxes-filled-by-sqlite/](https://www.pipiscrew.com/2016/02/android-listview-w-checkboxes-filled-by-sqlite/)</frag_product></frag_product></frag_product></frag_product>

origin - http://www.pipiscrew.com/?p=4105 android-listview-with-custom-adapter-viewholder