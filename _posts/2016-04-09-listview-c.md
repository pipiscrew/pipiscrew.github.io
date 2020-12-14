---
title: listview colorize subitems
author: PipisCrew
date: 2016-04-09
categories: [.net]
toc: true
---

![snap142](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap142.png)

```js
//test.cs

string[] dr = Directory.GetDirectories(txtStartDir.Text);

ListViewItem lv = null;

foreach (string item in dr)
{
    lv = new ListViewItem(item);

    //you must set this to ListViewItem
    lv.UseItemStyleForSubItems = false;

    lv.SubItems.Add("0");
    lv.SubItems.Add("0");
    lv.SubItems.Add("Ready to go!");
    lv.Checked = true;

    lstv.Items.Add(lv);
}

//on button click - get only the checked
foreach (ListViewItem item in lstv.CheckedItems)
{
	item.SubItems[1].Text = Directory.GetFiles(item.Text, "*.pdf").Count().ToString();
	item.SubItems[2].Text = Directory.GetDirectories(item.Text).Count().ToString();

	//then::
	item.SubItems[2].BackColor = Color.Red;
	item.SubItems[2].ForeColor = Color.Yellow;
}
```

origin - http://www.pipiscrew.com/?p=4842 net-listview-colorize-subitems