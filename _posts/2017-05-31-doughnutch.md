---
title: DoughnutChartView
author: PipisCrew
date: 2017-05-31
categories: [android]
toc: true
---

![Snap56](https://www.pipiscrew.com/wp-content/uploads/2016/02/Snap56.png)

```js
//MainActivity.java
import android.app.Activity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuInflater;
import android.widget.TextView;

public class MainActivity extends Activity {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.maind);

		DoughnutChartView x = (DoughnutChartView) findViewById(R.id.doughnut_chart);
		x.setTotalAmount(60);

		int[] arrayOfInt2 = new int[4];
		arrayOfInt2[0] = MainActivity.this.getResources().getColor(R.color.pie_income_1);
		arrayOfInt2[1] = MainActivity.this.getResources().getColor(R.color.pie_income_2);
		arrayOfInt2[2] = MainActivity.this.getResources().getColor(R.color.pie_income_3);
		arrayOfInt2[3] = MainActivity.this.getResources().getColor(R.color.pie_income_4);

		x.setProgressColorList(arrayOfInt2);

		double[] arrayOfDouble = new double[4];
		arrayOfDouble[0] = 30;
		arrayOfDouble[1] = 10;
		arrayOfDouble[2] = 10;
		arrayOfDouble[3] = 10;

		x.setCirclePieAmountList(arrayOfDouble);

		TextView c1 = (TextView) findViewById(R.id.doughtnut_chart_color1);
		c1.setBackgroundResource(R.color.pie_income_1);

		c1 = (TextView) findViewById(R.id.doughtnut_chart_text1);
		c1.setText("asdf1");

		TextView c2 = (TextView) findViewById(R.id.doughtnut_chart_color2);
		c2.setBackgroundResource(R.color.pie_income_2);

		c2 = (TextView) findViewById(R.id.doughtnut_chart_text2);
		c2.setText("asdf2");

		TextView c3 = (TextView) findViewById(R.id.doughtnut_chart_color3);
		c3.setBackgroundResource(R.color.pie_income_3);

		c3 = (TextView) findViewById(R.id.doughtnut_chart_text3);
		c3.setText("asdf3");

		TextView c4 = (TextView) findViewById(R.id.doughtnut_chart_color4);
		c4.setBackgroundResource(R.color.pie_income_4);

		c4 = (TextView) findViewById(R.id.doughtnut_chart_text4);
		c4.setText("asdf4");
	}
}
```

```js
//DoughnutChartView.java
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Paint;
import android.graphics.RectF;
import android.os.Bundle;
import android.os.Parcelable;
import android.util.AttributeSet;
import android.view.View;

public class DoughnutChartView extends View {
    private boolean fpa;
    private int fpb;
    private final RectF fpc;
    private float fpd;
    private int[] fpe;
    private double fpf;
    private double[] fpg;
    private final Paint fph;
    private final int fpi;
    private int fpj;
    private int fpk;
    private float fpl;
    private float fpm;

    public DoughnutChartView(Context arg2) {
        this(arg2, null);
    }

    public DoughnutChartView(Context arg4, AttributeSet arg5) {
        super(arg4, arg5);
        this.fpa = true;
        this.fpb = 10;
        this.fpc = new RectF();
        this.fpj = 0;
        this.fpk = 0;
        this.setWheelSize(20);
        this.fpi = 1;
        this.fph = new Paint(1);
        this.fph.setStyle(Paint.Style.STROKE);
        this.fph.setStrokeWidth(((float)this.fpb));
        this.fpa = false;
    }

    public double[] getCirclePieAmountList() {
        return this.fpg;
    }

    public int[] getProgressColorList() {
        return this.fpe;
    }

    public double getTotalAmount() {
        return this.fpf;
    }

    private float mpa(double arg5) {
    	   if (this.fpf == 0.0D) {
    		      return 0.0F;
    		    }
    		    return (float)(360.0D * arg5 / this.fpf);
    }

    private void mpa(int arg4, int arg5) {
        int v0 = this.fpi;
        switch(v0 & 7) {
            case 3: {
                this.fpj = 0;
                break;
            }
            case 5: {
                this.fpj = arg4;
                break;
            }
            default: {
                this.fpj = arg4 / 2;
                break;
            }
        }

        switch(v0 & 112) {
            case 48: {
                this.fpk = 0;
                break;
            }
            case 80: {
                this.fpk = arg5;
                break;
            }
            default: {
                this.fpk = arg5 / 2;
                break;
            }
        }
    }

    protected void onDraw(Canvas arg13) {
        float v11 = 1f;
        double v0 = 0;
        if(this.fpf != v0 && this.fpg.length != 0) {
            arg13.translate(this.fpl, this.fpm);
            int v9 = this.fpg.length;
            float v2 = 270f;
            int v6 = 0;
            double v7 = v0;
            while(v6 < v9)="" {="" this.fph.setcolor(this.fpe[v6]);="" float="" v10="this.mpa(this.fpg[v6]);" arg13.drawarc(this.fpc,="" v2,="" v10="" -="" v11,="" false,="" this.fph);="" float="" v3="v2" +="" v10;="" double="" v1="v7" +="" this.fpg[v6];="" ++v6;="" v7="v1;" v2="v3;" }="" if(this.fpf=""> v7) {
                float v0_1 = this.mpa(this.fpf - v7);
                this.fph.setColor(this.fpe[3]);
                arg13.drawArc(this.fpc, v2, v0_1 - v11, false, this.fph);
            }
        }
    }

    protected void onMeasure(int arg10, int arg11) {
        int v0 = DoughnutChartView.getDefaultSize(this.getSuggestedMinimumHeight(), arg11);
        int v1 = DoughnutChartView.getDefaultSize(this.getSuggestedMinimumWidth(), arg10);
        int v2 = Math.min(v1, v0);
        this.setMeasuredDimension(v2, v0);
        float v3 = 0.5f * (((float)v2));
        this.fpd = v3 - (((float)this.fpb));
        this.fpc.set(-this.fpd, -this.fpd, this.fpd, this.fpd);
        this.mpa(v1 - v2, v0 - v2);
        this.fpl = (((float)this.fpj)) + v3;
        this.fpm = (((float)this.fpk)) + v3;
    }

    protected void onRestoreInstanceState(Parcelable paramParcelable)
    {
      if ((paramParcelable instanceof Bundle))
      {
        super.onRestoreInstanceState(((Bundle)paramParcelable).getParcelable("saved_state"));
        return;
      }
      super.onRestoreInstanceState(paramParcelable);
    }

    protected Parcelable onSaveInstanceState() {
        Bundle v0 = new Bundle();
        v0.putParcelable("saved_state", super.onSaveInstanceState());
        v0.putFloat("progress", 180f);
        return ((Parcelable)v0);
    }

    public void setCirclePieAmountList(double[] arg1) {
        this.fpg = arg1;
    }

    public void setProgressColorList(int[] arg1) {
        this.fpe = arg1;
    }

    public void setTotalAmount(double arg1) {
        this.fpf = arg1;
    }

    private void setWheelSize(int arg1) {
        this.fpb = arg1;
    }
}
```

the xml :
```js
//drawable/card_now_style_drawable.xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android"></selector>

//values/colors.xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="pie_income_1">#ff8abd00</color>
    <color name="pie_income_2">#ffa8d324</color>
    <color name="pie_income_3">#ffc5e26d</color>
    <color name="pie_income_4">#ffe2f0b6</color>

    <color name="pie_expense_1">#ffff5f5f</color>
    <color name="pie_expense_2">#ffff8686</color>
    <color name="pie_expense_3">#ffffafaf</color>
    <color name="pie_expense_4">#ffffcaca</color>
</resources>

//values/styles.xml

    <style name="TextAppearance" parent="@android:style/TextAppearance">

    <style name="TextAppearance.EditEvent_Small" parent="@style/TextAppearance">
        <item name="android:textAppearance">?android:textAppearanceSmall</item>
        <item name="android:textSize">@dimen/text_size_small</item>
        <item name="android:textColor">#ffaaaaaa</item>
    </style>

    <style name="TextAppearance.SliderHeadingAppearance" parent="@style/TextAppearance.EditEvent_Small">
        <item name="android:textStyle">bold</item>
    </style>

    <style name="TextAppearance.EditEvent_LabelSmall" parent="@style/TextAppearance.EditEvent_Small">
        <item name="android:paddingLeft">8.0dip</item>
        <item name="android:paddingRight">8.0dip</item>
        <item name="android:paddingBottom">8.0dip</item>
        <item name="android:layout_width">144.0dip</item>
        <item name="android:layout_marginLeft">16.0dip</item>
        <item name="android:layout_marginRight">16.0dip</item>
        <item name="android:minHeight">24.0dip</item>
    </style>

    <style name="TagTextAppearance" parent="@android:style/Widget.TextView">
        <item name="android:minHeight">48.0dip</item>
    </style>

    <style name="nowCardStyle" parent="@android:style/Widget.TextView">
        <item name="android:gravity">center</item>
        <item name="android:background">@drawable/card_now_style_drawable</item>
        <item name="android:padding">@dimen/now_card_style_padding</item>
    </style>

//values/dimens.xml
<resources>

    <dimen name="activity_horizontal_margin">16dp</dimen>
    <dimen name="activity_vertical_margin">16dp</dimen>

        <dimen name="alp_lockpatternview_max_size">400.0dip</dimen>
    <dimen name="default_circle_indicator_radius">3.0dip</dimen>
    <dimen name="default_circle_indicator_stroke_width">1.0dip</dimen>
    <dimen name="default_line_indicator_line_width">12.0dip</dimen>
    <dimen name="default_line_indicator_gap_width">4.0dip</dimen>
    <dimen name="default_line_indicator_stroke_width">1.0dip</dimen>
    <dimen name="default_title_indicator_clip_padding">4.0dip</dimen>
    <dimen name="default_title_indicator_footer_line_height">2.0dip</dimen>
    <dimen name="default_title_indicator_footer_indicator_height">4.0dip</dimen>
    <dimen name="default_title_indicator_footer_indicator_underline_padding">20.0dip</dimen>
    <dimen name="default_title_indicator_footer_padding">7.0dip</dimen>
    <dimen name="default_title_indicator_text_size">15.0dip</dimen>
    <dimen name="default_title_indicator_title_padding">5.0dip</dimen>
    <dimen name="default_title_indicator_top_padding">7.0dip</dimen>
    <dimen name="actionbar_compat_height">45.0dip</dimen>
    <dimen name="text_size_extra_tiny">12.0sp</dimen>
    <dimen name="text_size_tiny">13.0sp</dimen>
    <dimen name="text_size_small">15.0sp</dimen>
    <dimen name="text_size_medium">18.0sp</dimen>
    <dimen name="text_size_large">22.0sp</dimen>
    <dimen name="transaction_row_size_tiny">13.0sp</dimen>
    <dimen name="transaction_row_size_small">15.0sp</dimen>
    <dimen name="transaction_row_size_medium">18.0sp</dimen>
    <dimen name="text_size_extra_large">26.0sp</dimen>
    <dimen name="summary_left_padding">8.0dip</dimen>
    <dimen name="pane_seperator_width">1.0dip</dimen>
    <dimen name="tiny_seperator">0.5dip</dimen>
    <dimen name="tab_text_padding">16.0dip</dimen>
    <dimen name="reminders_list_padding_side">8.0dip</dimen>
    <dimen name="reminders_date_margin_right">5.0dip</dimen>
    <dimen name="amount_reminder_width">80.0dip</dimen>
    <dimen name="doughnut_chart_size">150.0dip</dimen>
    <dimen name="due_date_btn_width">125.0dip</dimen>
    <dimen name="item_height">67.0dip</dimen>
    <dimen name="due_time_btn_width">90.0dip</dimen>
    <dimen name="widget_margin">20.0dip</dimen>
    <dimen name="large_widget_margin">20.0dip</dimen>
    <dimen name="sign_elements_padding">16.0dip</dimen>
    <dimen name="widget_padding_margin">8.0dip</dimen>
    <dimen name="slidingmenu_marginLeft">8.0dip</dimen>
    <dimen name="form_grid_marginRight">8.0dip</dimen>
    <dimen name="form_grid_marginBottom">4.0dip</dimen>
    <dimen name="transaction_image_disp_size">150.0dip</dimen>
    <dimen name="slidingmenu_width">250.0dip</dimen>
    <dimen name="shadow_width">15.0dip</dimen>
    <dimen name="list_padding">10.0dip</dimen>
    <dimen name="now_card_style_padding">25.0dip</dimen>
    <dimen name="left_line_chart_label_width">64.0dip</dimen>
    <dimen name="summary_page_padding">8.0dip</dimen>
</resources>

```

origin - http://www.pipiscrew.com/?p=3773 android-doughnutchartview