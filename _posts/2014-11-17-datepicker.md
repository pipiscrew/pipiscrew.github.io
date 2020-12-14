---
title: DatePickerFragment + Interface
author: PipisCrew
date: 2014-11-17
categories: []
toc: true
---

reference :
[http://developer.android.com/guide/topics/ui/controls/pickers.html](http://developer.android.com/guide/topics/ui/controls/pickers.html)
[http://www.javacodegeeks.com/2013/06/android-fragment-transaction-fragmentmanager-and-backstack.html](http://www.javacodegeeks.com/2013/06/android-fragment-transaction-fragmentmanager-and-backstack.html)
[Samsung nexus glass repair i9250](http://www.youtube.com/user/krsolutions/search?query=samsung)

> the activity call

```js
public class AutoMotoDetails extends Activity {

	Button btn_date = null;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_auto_moto_details);

		btn_date = (Button) findViewById(R.id.btn_date);
		btn_date.setText(General.get_now());
	}

	public void showDatePickerDialog(View v) {
		FragmentTransaction ft = AutoMotoDetails.this.getFragmentManager().beginTransaction();
		DatePickerFragment newFragment = new DatePickerFragment();

		// //////////////////////////////////////////// Parse date from button text
		Date d = General.get_date_from_string(btn_date.getText().toString());
		Calendar cal = Calendar.getInstance();
		cal.setTime(d);
		int year = cal.get(Calendar.YEAR);
		int month = cal.get(Calendar.MONTH);
		int day = cal.get(Calendar.DAY_OF_MONTH);

		// //////////////////////////////////////////// Create a bundle
		Bundle currentDate = new Bundle();
		currentDate.putInt("y", year);
		currentDate.putInt("d", day);
		currentDate.putInt("m", month);

		// //////////////////////////////////////////// Set bundle to fragment
		newFragment.setArguments(currentDate);

		// //////////////////////////////////////////// Event listener user choice		
		newFragment.setListener(new DatePickerFragmentListener() {
			@Override
			public void datepicked(String user_date) {
				btn_date.setText(user_date);
			}

		});

		// //////////////////////////////////////////// Show fragment
		newFragment.show(ft, "dialog");
	}

//where General.get_date_from_string
	public static Date get_date_from_string(String dT){
		try{
			SimpleDateFormat sDT = new SimpleDateFormat("dd/MM/yyyy");
			return sDT.parse(dT);
			}catch(Exception ex){
				return null;
			}
	}

//where at XML
<button android:id="@+id/btn_date" android:layout_width="wrap_content" android:layout_height="wrap_content" android:text="date" android:onclick="showDatePickerDialog"></button>
```

> DatePickerFragment.java

```js
import java.util.EventListener;
import android.app.DatePickerDialog;
import android.app.Dialog;
import android.app.DialogFragment;
import android.os.Bundle;
import android.widget.DatePicker;

public class DatePickerFragment extends DialogFragment implements DatePickerDialog.OnDateSetListener {

	// ////////////////////////////////////////////////////////////////////////////
	// Used to transfer back the result
	private DatePickerFragmentListener listener;

	public interface DatePickerFragmentListener extends EventListener {
		public void datepicked(String user_date);
	}

	public void setListener(DatePickerFragmentListener listener) {
		this.listener = listener;
	}

	// ////////////////////////////////////////////////////////////////////////////

	@Override
	public Dialog onCreateDialog(Bundle savedInstanceState) {
		Bundle setDate = this.getArguments();
		int year = setDate.getInt("y");
		int day = setDate.getInt("d");
		int month = setDate.getInt("m");

		// Create a new instance of DatePickerDialog and return it
		return new DatePickerDialog(getActivity(), this, year, month, day);
	}

	public void onDateSet(DatePicker view, int year, int month, int day) {
		// month is zero based here!
		String dT = String.valueOf(day) + "/" + String.valueOf(month + 1) + "/" + String.valueOf(year);
		listener.datepicked(dT);
	}
}
```

origin - http://www.pipiscrew.com/?p=1899 android-datepickerfragment-interface