---
title: Google Charts
author: PipisCrew
date: 2017-02-08
categories: [js,php]
toc: true
---

### Pie Chart

ref - https://google-developers.appspot.com/chart/interactive/docs/gallery/piechart
using the ^page sample, at legends doesnt write the value, use the following fix by Fabio Cordeiro
```js
//http://stackoverflow.com/a/37333511

      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);
      function drawChart() {

		var data = google.visualization.arrayToDataTable(<?= json_encode($countries);?>);

        var total = 0;
        for (var i = 0; i < data.getNumberOfRows(); i++) {
            total = total + data.getValue(i, 1);    
        }

        for (var i = 0; i < data.getNumberOfRows(); i++) {
                var label = data.getValue(i, 0);
            var val = data.getValue(i, 1) ;
            var percentual = ((val / total) * 100).toFixed(1); 
            data.setFormattedValue(i, 0, label  + ' - '+val +' ('+ percentual + '%)');    
        }

        var options = {
          title: 'Tickets Per Country'
        };

        var chart = new google.visualization.PieChart(document.getElementById('piechart'));

        chart.draw(data, options);
      }

    <div id="piechart" style="width: 900px; height: 800px;"></div>

```

or you can draw lines and show the values adding this to options :
```js
//http://stackoverflow.com/a/19181740
legend: {
    position: 'labeled'
}
```

### Fixing the bootstrap nav-tabs when displaying Google Chart(s) on more than 1 tab

```js
//src - http://stackoverflow.com/a/30468366
<?php fill="" $result="" with="" a="" pdo="" recordset="" $countries="array();" $countries[]="array('Country'," 'hits="" per="" day');="" foreach($result="" as="" $row)="" {="" $countries[]="array($row[0]['country']," sizeof($row));="" }="" fill="" $result2="" with="" a="" pdo="" recordset="" $users="array();" $users[]="array('Users'," 'hits="" per="" day');="" foreach($result2="" as="" $row)="" {="" $users[]="array($row[0]['users']," sizeof($row));="" }=""?>

        //output charts to PNG - https://developers.google.com/chart/interactive/docs/printing

        $(function() {

        	//fix to draw or redraw when user switch tab 
            $('a[data-toggle="tab"]').on('shown.bs.tab', function (e) {
                //http://stackoverflow.com/a/30468366

                //draw the pies TAB1
                if (this.href.indexOf('#countries')>0){
		          byCountryPIE();
		          //any other chart for 1st tab.
		          //byCountrySoftwaresPIE();
		          //byCountryCompaniesPIE();
                }

                //draw the pies TAB2
                if (this.href.indexOf('#users')>0){
                  byUserPIE();
                  //any other chart for 2nd tab.
                  //byUserSoftwaresPIE();
                  //byUserCompaniesPIE();
                }

            })

        });

      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(draw_pies);

      //triggered only by^
      function draw_pies(){
          byCountryPIE();
          //any other chart for 1st tab.
          //byCountrySoftwaresPIE();
          //byCountryCompaniesPIE();
      }

    /////////////////////////////
    //byCountryPIE
    function byCountryPIE() {

		var data = google.visualization.arrayToDataTable(<?= json_encode($countries);?>);

        //fix to display the value in legend
        var total = 0;
        for (var i = 0; i < data.getNumberOfRows(); i++) {
                total = total + data.getValue(i, 1);    
        }

        for (var i = 0; i < data.getNumberOfRows(); i++) {
                var label = data.getValue(i, 0);
            var val = data.getValue(i, 1) ;
            var percentual = ((val / total) * 100).toFixed(1); 
            data.setFormattedValue(i, 0, label  + ' - '+val +' ('+ percentual + '%)');    
        }
        //fix to display the value in legend

        var options = {
          title: 'Tickets Per Country'
        };

        var chart = new google.visualization.PieChart(document.getElementById('byCountryPIE'));

        chart.draw(data, options);
      }

//------------USERS------------

    /////////////////////////////
    //byUserPIE
    function byUserPIE() {

		var data = google.visualization.arrayToDataTable(<?= json_encode($users);?>);

        //fix to display the value in legend
        var total = 0;
        for (var i = 0; i < data.getNumberOfRows(); i++) {
                total = total + data.getValue(i, 1);    
        }

        for (var i = 0; i < data.getNumberOfRows(); i++) {
                var label = data.getValue(i, 0);
            var val = data.getValue(i, 1) ;
            var percentual = ((val / total) * 100).toFixed(1); 
            data.setFormattedValue(i, 0, label  + ' - '+val +' ('+ percentual + '%)');    
        }
        //fix to display the value in legend

        var options = {
          title: 'Tickets Per User'
        };

        var chart = new google.visualization.PieChart(document.getElementById('byUserPIE'));

        chart.draw(data, options);
      }

<div class="container-fluid">

*   [Countries](#countries)        

*   [Users](#users)

*   [About](#about)

    <div class="tab-content">
      <div id="countries" class="tab-pane fade in active">
            <div class="row">
                <div class="col-md-6">
                	<div id="byCountryPIE" style="width: 1000px; height: 800px;"></div>
                </div>

            </div>
      </div>
      <div id="users" class="tab-pane fade">
            <div class="row">
                <div class="col-md-6">
                	<div id="byUserPIE" style="width: 1000px; height: 800px;"></div>
                </div>
            </div>
      </div>
      <div id="about" class="tab-pane fade">
            <div class="row">
                    pipiscrew sample
            </div>
      </div>
    </div>

</div>

```

* * *

### dynamic add columns to Google Bar Chart!

reference 
[http://google-developers.appspot.com/chart/interactive/docs/gallery/columnchart](http://google-developers.appspot.com/chart/interactive/docs/gallery/columnchart)

[![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap386.png "snap386")](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap386.png)

```js
//sample1
<?php $chart_row_setup="array();" $chart_columns_setup="array();" $chart_columns_setup[]="Type" ;="" $chart_columns_setup[]="Income" ;="" $chart_columns_setup[]="Expenses" ;="" $chart_columns_setup[]="NET" ;="" chart="" legend="" $chart_row_setup[0]="$chart_columns_setup;" for="" ($i=""?><12;$i++){ $col_vals="array();" $col_vals[]="monthName($i);" $col_vals[]="(int)$ListOfBalanceRECS[$i]-">income;
	$col_vals[]=(int)$ListOfBalanceRECS[$i]->expense;
	$col_vals[]=(int)$ListOfBalanceRECS[$i]->net;

	$chart_row_setup[] = $col_vals;
}
?>

      google.load("visualization", "1.1", {packages:["bar"]});
      google.setOnLoadCallback(drawChart);
      function drawChart() {
        var data = google.visualization.arrayToDataTable(<?= json_encode($chart_row_setup);?>);

        var options = {
          chart: {
            title: 'Company Performance',
            subtitle: 'Sales, Expenses and Profit',
          }
        };

        var chart = new google.charts.Bar(document.getElementById('columnchart_material'));

         chart.draw(data, options);
        }

```

```js
//sample2
<?php get="" users="" $chart_db_users="getSet($db," select"="" user_id,fullname="" from="" users="" where="" user_level_id="" in="" (31,42,59)",null);="" $chart_row_setup="array();" $chart_columns_setup="array();" $chart_columns_setup[]="Month" ;="" for(="" $i="0" ;="" $i=""?><= sizeof($chart_db_users)-1="" ;="" $i++="" )="" {="" $chart_columns_setup[]="$chart_db_users[$i][" fullname"];"="" }="" always="" on="" 0="" array="" position="" are="" the="" bar="" names="" $chart_row_setup[0]="$chart_columns_setup;" below="" merge="" the="" bars="" values="" $col_vals="array();" for="" each="" month="" for(="" $m="1" ;="" $m=""></=><= 12="" ;="" $m++="" )="" {="" $col_vals="array();" $col_vals[]="monthName($m);" construct="" valid="" date="" for="" mysql="" if=""></=><10) {="" $start="date(" y-0{$m}-01");"="" $end="get_end_of_the_month($m,date('Y'));" }="" else="" {="" $start="date(" y-{$m}-01");"="" $end="get_end_of_the_month($m,date('Y'));" }="" for="" each="" user="" for(="" $i="0" ;="" $i=""></10)><= sizeof($chart_db_users)-1="" ;="" $i++="" )="" {="" query="" with="" date="" between="" depends="" on="" $m="" variable="" $col_vals[]="(int)" getscalar($db,"select="" count(offer_id)="" from="" offers="" where="" offer_seller_id=".$chart_db_users[$i]['user_id']." and="" offer_proposal_date="" between="" '".$start."'="" and="" '".$end."'",null);="" }="" $chart_row_setup[]="$col_vals;" }="" http://edpriceishungry.com/2010/01/04/converting-integers-to-monthnames-in-php/="" function="" monthname($month_int)="" {="" $month_int="(int)$month_int;" $timestamp="mktime(0," 0,="" 0,="" $month_int);="" return="" date(“f”,="" $timestamp);="" }="" function="" get_end_of_the_month($month,="" $year)="" {="" if="" (strlen($month)="=1)" $month="0" .$month;="" t="" returns="" the="" number="" of="" days="" in="" the="" month="" of="" a="" given="" date="" $d="date(" t","="" strtotime(date("{$year}-{$month}-d")));="" $m="date(" {$year}-{$month}-{$d}");"="" format="" back="" to="" mysql="" style!="" return="" $m;="" }=""></=>

//pass array to javascript

      google.load("visualization", "1.1", {packages:["bar"]});
      google.setOnLoadCallback(drawChart);
      function drawChart() {
        var data = google.visualization.arrayToDataTable(<?= json_encode($chart_row_setup);?>);

        var options = {
          chart: {
            title: 'Company Performance',
            subtitle: 'Sales, Expenses, and Profit: 2014-2017',
          }
        };

        var chart = new google.charts.Bar(document.getElementById('columnchart_material'));

        chart.draw(data, options);
      }

```

![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap336.png "snap336")</12;$i++){>

origin - http://www.pipiscrew.com/?p=2115 php-google-charts