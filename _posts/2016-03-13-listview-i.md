---
title: listview into scrollview
author: PipisCrew
date: 2016-03-13
categories: [android]
toc: true
---

-Fix listview item height with **General.setListViewHeightBasedOnChildren**
-Scrollview can grow with **fillViewport**
-Scroll to Top

WARNING the listview_item.xml (filled on adapter) MUST contains LinearLayouts non Relatives. On old devices users got 

> java.lang.NullPointerException at android.widget.RelativeLayout.onMeasure(RelativeLayout.java)

```js
//source - http://stackoverflow.com/a/8406253/1320686
<scrollview android:id="@+id/product_detail_scrollView" android:layout_width="match_parent" android:layout_height="wrap_content" android:layout_below="@+id/product_details" android:fillviewport="true">

        <relativelayout android:layout_width="wrap_content" android:layout_height="wrap_content">
.
.
		<listview android:id="@+id/product_detail_lstv" android:layout_width="match_parent" android:layout_height="wrap_content" android:focusable="false" android:layout_below="@+id/x" android:layout_marginbottom="2dip" android:divider="#c4cacb" android:dividerheight="2dp"></listview>
	</relativelayout>
</scrollview>
```

```js
...fill listview
.
..
} finally {
	lstv_adapter.notifyDataSetChanged();

	//scroll to top
	((ScrollView) findViewById(R.id.product_detail_scrollView)).smoothScrollTo(0,0);

	//fix listview height
	General.setListViewHeightBasedOnChildren(lstv);
}

public final class General {

    public static void setListViewHeightBasedOnChildren(ListView listView) {
        ListAdapter listAdapter = listView.getAdapter(); 
        if (listAdapter == null) {
            // pre-condition
            return;
        }

        int totalHeight = 0;
        for (int i = 0; i < listadapter.getcount(); i++) {
            view listitem = listadapter.getview(i, null, listview);
            listitem.measure(0, 0);
            totalheight += listitem.getmeasuredheight();
        }

        viewgroup.layoutparams params = listview.getlayoutparams();
        params.height = totalheight + (listview.getdividerheight() * (listadapter.getcount() - 1));
        listview.setlayoutparams(params);
        listview.requestlayout();
    }     
}

``` listadapter.getcount();="" i++)="" {="" view="" listitem="listAdapter.getView(i," null,="" listview);="" listitem.measure(0,="" 0);="" totalheight="" +="listItem.getMeasuredHeight();" }="" viewgroup.layoutparams="" params="listView.getLayoutParams();" params.height="totalHeight" +="" (listview.getdividerheight()="" *="" (listadapter.getcount()="" -="" 1));="" listview.setlayoutparams(params);="" listview.requestlayout();="" }="" }=""></ listadapter.getcount(); i++) {
            view listitem = listadapter.getview(i, null, listview);
            listitem.measure(0, 0);
            totalheight += listitem.getmeasuredheight();
        }

        viewgroup.layoutparams params = listview.getlayoutparams();
        params.height = totalheight + (listview.getdividerheight() * (listadapter.getcount() - 1));
        listview.setlayoutparams(params);
        listview.requestlayout();
    }     
}

```>

origin - http://www.pipiscrew.com/?p=4392 android-listview-into-scrollview