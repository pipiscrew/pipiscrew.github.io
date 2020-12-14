---
title: edittext with checkbox into alertdialog
author: PipisCrew
date: 2015-08-18
categories: [android]
toc: true
---

reference 
http://developer.android.com/reference/android/widget/CheckBox.html
multicheckboxes - [http://www.learn-android-easily.com/2013/01/adding-check-boxes-in-dialog.html](http://www.learn-android-easily.com/2013/01/adding-check-boxes-in-dialog.html)
radiobuttons - [http://developer.android.com/guide/topics/ui/controls/radiobutton.html](http://developer.android.com/guide/topics/ui/controls/radiobutton.html)

```js
AlertDialog.Builder builder = new AlertDialog.Builder(this, R.style.AppBaseTheme);
builder.setTitle("Alert Title");

final EditText input = new EditText(this);
final CheckBox chkENG2GR = new CheckBox(this);
chkENG2GR.setText("ENG2GR");

// Set up the buttons
builder.setPositiveButton("save", new DialogInterface.OnClickListener() {
	@Override
	public void onClick(DialogInterface dialog, int which) {
	if (chkENG2GR.isChecked()) {
		//is checked
	}
	else {
		//is unchecked
	}

	}

builder.setNegativeButton("cancel", new DialogInterface.OnClickListener() {
	@Override
	public void onClick(DialogInterface dialog, int which) {
		dialog.cancel();
	}
});

LinearLayout linearLayout = new LinearLayout(this);
linearLayout.setLayoutParams(new LinearLayout.LayoutParams(LinearLayout.LayoutParams.FILL_PARENT, LinearLayout.LayoutParams.FILL_PARENT));
linearLayout.setOrientation(1);
linearLayout.addView(input); //add editext
linearLayout.addView(chkENG2GR); //add checkbox

builder.show();
```

origin - http://www.pipiscrew.com/?p=1544 android-edittext-with-checkbox-into-alertdialog