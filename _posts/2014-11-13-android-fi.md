---
title: android findViewById2014
author: PipisCrew
date: 2014-11-13
categories: []
toc: true
---

```js
((CheckBox)findViewById(R.id.cbAutoSync)).setChecked(autSync);

findViewById(R.id.btnShowRemoteList).setEnabled(true);

findViewById(R.id.btnClearLocalData).setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v) {
		Toast.makeText(Main.this, "test", Toast.LENGTH_SHORT).show();
	}
});
```

origin - http://www.pipiscrew.com/?p=1851 android-findviewbyid2014