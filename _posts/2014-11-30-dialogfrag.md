---
title: dialogfragment - save state + retain listener
author: PipisCrew
date: 2014-11-30
categories: []
toc: true
---

reference
[http://developer.android.com/reference/android/app/Activity.html](http://developer.android.com/reference/android/app/Activity.html)
[http://android-er.blogspot.com/2011/09/onsaveinstancestate-and.html](http://android-er.blogspot.com/2011/09/onsaveinstancestate-and.html)

> onSaveInstanceState() - used for save state of the UI
> onPause() - used to store persistent data

Normally we use the onPause() to store any data then on onCreate/onCreateView restore it, what about in a dialogfragment that we have an interface (listener)
```js
public class AutoMotoDetailsFrag extends DialogFragment implements OnClickListener {

private AutoMotoDetailsFragListener listener;
.
.
.

	@Override
	public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
		View view = inflater.inflate(R.layout.automotodetailsfrag, container);

		setupGUI(view);

		if (savedInstanceState != null) {
			SharedPreferences mPrefs = c.getSharedPreferences("automotodetailsfrag", 0);
			parent_id = mPrefs.getString("parent_id", null);
			id = mPrefs.getString("id", null);
			btn_date.setText(mPrefs.getString("btn_date", ""));
			btn_km.setText(mPrefs.getString("btn_km", ""));
			txt_cst.setText(mPrefs.getString("txt_cst", ""));
			txt_place.setText(mPrefs.getString("txt_place", ""));
			txt_fixes.setText(mPrefs.getString("txt_fixes", ""));
		}
	}

	@Override
	public void onPause()
	{
	        super.onPause();

	         SharedPreferences mPrefs = c.getSharedPreferences("automotodetailsfrag", 0); //0=mode_private
	         SharedPreferences.Editor ed = mPrefs.edit();
	         ed.putString("parent_id", parent_id);
	         ed.putString("id", id);
	         ed.putString("btn_date", btn_date.getText().toString());
	         ed.putString("btn_km", btn_km.getText().toString());
	         ed.putString("txt_cst", txt_cst.getText().toString());
	         ed.putString("txt_place", txt_place.getText().toString());
	         ed.putString("txt_fixes", txt_fixes.getText().toString());
	         ed.commit();
	}
}
```

//source by Luksprog : [http://stackoverflow.com/a/14044934](http://stackoverflow.com/a/14044934)
```js
//You update the listener reference in the onCreate method of the Activity:

private OnDateSetListener mOds = new OnDateSetListener() {

    @Override
    public void onDateSet(DatePicker view, int year, int monthOfYear,
            int dayOfMonth) {
             // do important stuff
    }
};
//and in the onCreate method:

if (savedInstanceState != null) {
    DatePickerFragment dpf = (DatePickerFragment) getSupportFragmentManager()
            .findFragmentByTag("theTag?");
    if (dpf != null) {
        dpf.setListener(mOds);
    }
}
```

//based on Luksprog solution, went to AutoMotoDetailsFrag *parent*
```js
public class AutoMotoDetails extends ExpandableListActivity implements OnChildClickListener {
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_auto_moto_details);

		if (savedInstanceState != null) {
			AutoMotoDetailsFrag dpf = (AutoMotoDetailsFrag) this.getFragmentManager().findFragmentByTag("automotodetails_frag");
			  if (dpf != null) {
			        dpf.setListener(new AutoMotoDetailsFragListener() {

						@Override
						public void inserted_id(String rec_id) {
							fill_list();
						}

					});
			    }
		}
	}

	//for the history - here is the show fragment procedure
	public void show_details(String record_id) {
		FragmentTransaction ft = this.getFragmentManager().beginTransaction();

		AutoMotoDetailsFrag newFragment = AutoMotoDetailsFrag.newInstance(record_id, parent_id);

		newFragment.setListener(new AutoMotoDetailsFragListener() {

			@Override
			public void inserted_id(String rec_id) {
				fill_list();
			}

		});

		newFragment.show(ft, "automotodetails_frag");
	}
}
```

origin - http://www.pipiscrew.com/?p=1941 android-dialogfragment-retain-listener