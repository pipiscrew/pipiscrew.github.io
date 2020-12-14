---
title: year expenses - organizer
author: PipisCrew
date: 2015-01-15
categories: []
toc: true
---

references 
datepicker - [http://www.malot.fr/bootstrap-datetimepicker/](http://www.malot.fr/bootstrap-datetimepicker/)
bootstrap-table - [http://wenzhixin.net.cn/p/bootstrap-table](http://wenzhixin.net.cn/p/bootstrap-table)

```js
//jq.validator custom method for combo
				$.validator.addMethod("greaterThanZero", function(value, element) {
				    return (value!=null && parseFloat(value) > 0);
				}, "* Amount must be greater than zero");	
```

```js

```

the tables :
```js
CREATE TABLE expense_categories (
  expense_category_id int(11) NOT NULL AUTO_INCREMENT,
  parent_id int(11) NOT NULL DEFAULT '0',
  expense_category_name varchar(100) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (expense_category_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

CREATE TABLE expense_templates (
  expense_template_id int(11) NOT NULL AUTO_INCREMENT,
  expense_category_id int(11) DEFAULT NULL,
  expense_sub_category_id int(11) DEFAULT NULL,
  price decimal(15,2) DEFAULT NULL,
  created_owner_id int(11) DEFAULT NULL,
  created_date datetime DEFAULT NULL,
  PRIMARY KEY (expense_template_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

CREATE TABLE expenses (
  expense_id int(11) NOT NULL AUTO_INCREMENT,
  expense_template_id int(11) DEFAULT NULL,
  cost decimal(15,2) DEFAULT NULL,
  pay_method int(11) DEFAULT NULL,
  daterec date DEFAULT NULL,
  comments varchar(150) COLLATE utf8_unicode_ci DEFAULT NULL,
  owner_id int(11) DEFAULT NULL,
  PRIMARY KEY (expense_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```

[![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap382.png "snap382")](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap382.png)

**the main.php :**
```js
//main.php
<?php session_start();="" if(!isset($_session["u"])){="" header("location:="" login.php");="" exit="" ;="" }="" else="" if($_session['level']="" !="-2){" die("you="" are="" not="" authorized="" to="" view="" this!");="" }="" include="" ('config.php');="" include="" ('config_general.php');="" $db="connect();" structured="" array="" class="" vrecord="" {="" public="" $exp_id;="" public="" $category;="" public="" $is_head;="" public="" $jan;="" public="" $jan_id;="" public="" $jan_suggested;="" public="" $feb;="" public="" $feb_id;="" public="" $feb_suggested;="" public="" $march;="" public="" $march_id;="" public="" $march_suggested;="" public="" $april;="" public="" $april_id;="" public="" $april_suggested;="" public="" $may;="" public="" $may_id;="" public="" $may_suggested;="" public="" $june;="" public="" $june_id;="" public="" $june_suggested;="" public="" $july;="" public="" $july_id;="" public="" $july_suggested;="" public="" $aug;="" public="" $aug_id;="" public="" $aug_suggested;="" public="" $sept;="" public="" $sept_id;="" public="" $sept_suggested;="" public="" $oct;="" public="" $oct_id;="" public="" $oct_suggested;="" public="" $nov;="" public="" $nov_id;="" public="" $nov_suggested;="" public="" $dec;="" public="" $dec_id;="" public="" $dec_suggested;="" }="" $listofrecs="array(vrecord);" $rec="null;" get="" all="" 'templates'="" aka="" (fixed="" costs)="" $categories="getSet($db," "select="" expense_template_id,cat.expense_category_name="" as="" cat,subcat.expense_category_name="" as="" sub,price="" from="" expense_templates="" left="" join="" expense_categories="" as="" cat="" on="" cat.expense_category_id="expense_templates.expense_category_id" left="" join="" expense_categories="" as="" subcat="" on="" subcat.expense_category_id="expense_templates.expense_sub_category_id" order="" by="" cat,sub",null);="" $prev_cat="" ;="" foreach($categories="" as="" $row)="" {="" $rec="new" vrecord();="" $rec-=""?>exp_id = $row['expense_template_id'];

	if ($prev_cat != $row['cat'])
		{

			//add dummy main category row!!
			$rec->exp_id =0;
			$rec->category = $row['cat'];
			$rec->is_head = 1;
			$rec->jan  = $rec->feb  = $rec->march = $rec->april = $rec->may  = $rec->june  = $rec->july  = $rec->aug  = $rec->sept  = $rec->oct  = $rec->nov = $rec->dec = "";
			$ListOfRECS[] = $rec;
			//add dummy main category row!!

			//add the real record!!
			$rec = new vrecord();
			$rec->category = $row['sub'];
			$rec->exp_id = $row['expense_template_id'];
			//add the real record!!
		}
	else 
	{	$rec->category = $row['sub'];
	}

		//query months 
		$y = date('Y');

		$jan = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-01-01' and '".get_end_of_the_month(01, $y)."' limit 1",null);
		$rec->jan = add_thousand($jan['cost'],2 );
		$rec->jan_id = $jan['expense_id'];
		$rec->jan_suggested = $row['price'];

		$feb = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-02-01' and '".get_end_of_the_month(02, $y)."' limit 1",null);
		$rec->feb = add_thousand($feb['cost'],2 );
		$rec->feb_id = $feb['expense_id'];
		$rec->feb_suggested = $row['price'];

		$march = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-03-01' and '".get_end_of_the_month(03, $y)."' limit 1",null);
		$rec->march = add_thousand($march['cost'],2 );
		$rec->march_id = $march['expense_id'];
		$rec->march_suggested = $row['price'];

		$april = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-04-01' and '".get_end_of_the_month(04, $y)."' limit 1",null);
		$rec->april = add_thousand($april['cost'],2 );
		$rec->april_id = $april['expense_id'];
		$rec->april_suggested = $row['price'];

		$may = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-05-01' and '".get_end_of_the_month(05, $y)."' limit 1",null);
		$rec->may = add_thousand($may['cost'],2 );
		$rec->may_id = $may['expense_id'];
		$rec->may_suggested = $row['price'];

		$june = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-06-01' and '".get_end_of_the_month(06, $y)."' limit 1",null);
		$rec->june = add_thousand($june['cost'],2 );
		$rec->june_id = $june['expense_id'];
		$rec->june_suggested = $row['price'];

		$july = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-07-01' and '".get_end_of_the_month(07, $y)."' limit 1",null);
		$rec->july = add_thousand($july['cost'],2 );
		$rec->july_id = $july['expense_id'];
		$rec->july_suggested = $row['price'];

		$aug = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-08-01' and '".get_end_of_the_month(08, $y)."' limit 1",null);
		$rec->aug = add_thousand($aug['cost'],2 );
		$rec->aug_id = $aug['expense_id'];
		$rec->aug_suggested = $row['price'];

		$sept = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-09-01' and '".get_end_of_the_month(09, $y)."' limit 1",null);
		$rec->sept = add_thousand($sept['cost'],2 );
		$rec->sept_id = $sept['expense_id'];
		$rec->sept_suggested = $row['price'];

		$oct = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-10-01' and '".get_end_of_the_month(10, $y)."' limit 1",null);
		$rec->oct = add_thousand($oct['cost'],2 );
		$rec->oct_id = $oct['expense_id'];
		$rec->oct_suggested = $row['price'];

		$nov = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-11-01' and '".get_end_of_the_month(11, $y)."' limit 1",null);
		$rec->nov = add_thousand($nov['cost'],2 );
		$rec->nov_id = $nov['expense_id'];
		$rec->nov_suggested = $row['price'];

		$dec = getRow($db,"select expense_id,sum(cost) as cost from expenses where expense_template_id = {$row['expense_template_id']} and daterec between '{$y}-12-01' and '".get_end_of_the_month(12, $y)."' limit 1",null);
		$rec->dec = add_thousand($dec['cost'],2 );
		$rec->dec_id = $dec['expense_id'];
		$rec->dec_suggested = $row['price'];
		//q months 

	$ListOfRECS[] = $rec;

	$prev_cat = $row['cat'];
}

$pay_methods = getSet($db, "select * from transaction_methods",null);

function add_thousand($val, $decimal)
{
	if ($val==null)
		return 0;
	else 
		return number_format( $val , $decimal , ',' , '.' );
}
?>

	$(function (){

			///////////////////////////////////////////////////////////// FILL pay_methods
			var jArray_pay_methods =   <?php echo json_encode($pay_methods); ?>;

			var combo_pay_methods = "<option value='0'></option>";
			for (var i = 0; i < jArray_pay_methods.length; i++)
			{
				combo_pay_methods += "<option value='" + jArray_pay_methods[i]["transaction_method_id"] + "'>" + jArray_pay_methods[i]["transaction_method_name"] + "</option>";
			}

			$("[name=pay_method]").html(combo_pay_methods);
			$("[name=pay_method]").change(); //select row 0 - no conflict on POST validation @ PHP
			///////////////////////////////////////////////////////////// FILL pay_methods

		    $('[name=daterec]').datetimepicker({
		        weekStart: 1,
		        todayBtn:  1,
				autoclose: 1,
				todayHighlight: 1,
				startView: 2,
				minView: 2,
				forceParse: 1
		    });

			var jArray = <?php echo json_encode($ListOfRECS); ?>;

			if (jArray)
			{
				var r ="";
				for(var no in jArray)	
				{
					//the first dummy record
					if (jArray[no]=="vrecord")
						continue;

					//template_id for table #expense_templates#
					r+= "<tr><td>"+jArray[no]["exp_id"]+"</td>";
					//each button has the ID for table #EXPENSES#

					//CATEGORY
					if ( jArray[no]["is_head"] == 1)
						{r+="<td>**"+jArray[no]["category"]+"**</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr>";
						continue;
						}
					else 
					{
						r+="<td><div style='margin-left:20px'>"+jArray[no]["category"]+"</div></td>";
					}

					////////////////////////////////////////////
					r+= create_button_for_month(jArray[no]["jan_suggested"],jArray[no]["jan"],jArray[no]["jan_id"],jArray[no]["exp_id"],"01");
					r+= create_button_for_month(jArray[no]["feb_suggested"],jArray[no]["feb"],jArray[no]["feb_id"],jArray[no]["exp_id"],"02");
					r+= create_button_for_month(jArray[no]["march_suggested"],jArray[no]["march"],jArray[no]["march_id"],jArray[no]["exp_id"],"03");
					r+= create_button_for_month(jArray[no]["april_suggested"],jArray[no]["april"],jArray[no]["april_id"],jArray[no]["exp_id"],"04");
					r+= create_button_for_month(jArray[no]["may_suggested"],jArray[no]["may"],jArray[no]["may_id"],jArray[no]["exp_id"],"05");
					r+= create_button_for_month(jArray[no]["june_suggested"],jArray[no]["june"],jArray[no]["june_id"],jArray[no]["exp_id"],"06");
					r+= create_button_for_month(jArray[no]["july_suggested"],jArray[no]["july"],jArray[no]["july_id"],jArray[no]["exp_id"],"07");
					r+= create_button_for_month(jArray[no]["aug_suggested"],jArray[no]["aug"],jArray[no]["aug_id"],jArray[no]["exp_id"],"08");
					r+= create_button_for_month(jArray[no]["sept_suggested"],jArray[no]["sept"],jArray[no]["sept_id"],jArray[no]["exp_id"],"09");
					r+= create_button_for_month(jArray[no]["oct_suggested"],jArray[no]["oct"],jArray[no]["oct_id"],jArray[no]["exp_id"],"10");
					r+= create_button_for_month(jArray[no]["nov_suggested"],jArray[no]["nov"],jArray[no]["nov_id"],jArray[no]["exp_id"],"11");
					r+= create_button_for_month(jArray[no]["dec_suggested"],jArray[no]["dec"],jArray[no]["dec_id"],jArray[no]["exp_id"],"12");
					r+="</tr>";

				}

				$("#exp_rows").html(r);
			}

			//http://wenzhixin.net.cn/p/bootstrap-table/docs/examples.html#via-javascript-table
			$('#expenses_tbl').bootstrapTable();

		    ////////////////////////////////////////
		    // MODAL FUNCTIONALITIES [START]
		    //when modal closed, hide the warning messages + reset
		    $('#modalEXPENSES').on('hidden.bs.modal', function() {
		        //when close - clear elements
		        $('#formEXPENSES').trigger("reset");

		        //clear validator error on form
		        validatorEXPENSES.resetForm();
		    });

		    //functionality when the modal already shown and its long, when reloaded scroll to top
		    $('#modalEXPENSES').on('shown.bs.modal', function() {
		        $(this).animate({
		            scrollTop : 0
		        }, 'slow');
		    });
		    // MODAL FUNCTIONALITIES [END]
		    ////////////////////////////////////////

			///////////////////////////////////// add custom validation
			//validate currency
			$.validator.addMethod('currency', function(value, element, regexp)
				{
					var re = /^\d{1,9}(\.\d{1,2})?$/;
					return this.optional(element) || re.test(value);
				}, '');

		    var validatorEXPENSES = $("#formEXPENSES").validate({
		        rules : {

		             cost : {required : true,
			                currency: true },
			          daterec : {required : true},
			          pay_method : {required : true,
			                greaterThanZero : true  }

		        },
		        messages : {
		            daterec : 'Required Field',
		            pay_method : 'Required Field',
		            cost : 'Required Field ex. 34.08'
		        }
		    });

			////////////////////////////////////////
			// MODAL SUBMIT aka save & update button
			$('#formEXPENSES').submit(function(e) {
			    e.preventDefault();

			    ////////////////////////// validation
			    var form = $(this);
			    form.validate();

			    if (!form.valid())
			        return;
			    ////////////////////////// validation

			    var postData = $(this).serializeArray();
			    var formURL = $(this).attr("action");

			    //close modal
			    $('#modalEXPENSES').modal('toggle');

			    $.ajax(
			    {
			        url : formURL,
			        type: "POST",
			        data : postData,
			        success:function(data, textStatus, jqXHR)
			        {
			            if (data=="00000")
							location.reload(true);
			            else
			                alert("ERROR");
			        },
			        error: function(jqXHR, textStatus, errorThrown)
			        {
			            alert("ERROR - connection error");
			        }
			    });
			});

	}) //jQuery ends

	function create_button_for_month(month_suggested,month,month_id,template_id,month_no){
			var template_btn = "<a style='width:100%' onclick='view_cost({suggested},{price},{exp_id},{edit},{template_id},{month_no});' class='btn btn-{paid} btn-xs'>{pay_price}</a>";

			var price_month = 0 ;

			if(month)
				 price_month = month.replace(',',".");

			var month_cell = template_btn.replace('{suggested}',month_suggested);
			month_cell = month_cell.replace('{price}',price_month);
			month_cell = month_cell.replace('{exp_id}',month_id);
			month_cell = month_cell.replace('{template_id}',template_id);
			month_cell = month_cell.replace('{month_no}',month_no);

			if (month==0){
				month_cell = month_cell.replace('{pay_price}',month_suggested);
				month_cell = month_cell.replace('{paid}',"danger");
				month_cell = month_cell.replace('{edit}',0);
			}

			else{
				month_cell = month_cell.replace('{pay_price}',price_month);
				month_cell = month_cell.replace('{paid}',"success");
				month_cell = month_cell.replace('{edit}',1);
			} 

			return "<td>"+month_cell+"</td>";
	}

	function view_cost(suggested,price,rec_id,is_edit,template_id,month_no)
	{

		$('[name=daterec]').datetimepicker('setStartDate', '<?=date("Y")?>-'+month_no+'-01');
		$('[name=daterec]').datetimepicker('setEndDate', getLastDateOfMonth(<?=date("Y")?>,month_no-1));

		$("#template_id").val(template_id);

		if (is_edit==1)
		{
			query_EXPENSES_modal(rec_id);

//			$('#lblTitle_EXPENSES').html("Edit Expense");
//			$("[name=cost]").val(price);
//			$("#expensesFORM_updateID").val(rec_id);
		}
		else
		{
			$('#lblTitle_EXPENSES').html("Add Expense");
			$("[name=cost]").val(suggested);
			$("[name=daterec]").val('01-'+twoDigits(month_no)+'-<?=date("Y")?>');//date_now4mysql());

			$('#modalEXPENSES').modal('toggle');
		}

	}

	//edit button - read record
	function query_EXPENSES_modal(rec_id){
		loading.appendTo(document.body);

	    $.ajax(
	    {
	        url : "fetch.php",
	        type: "POST",
	        data : { expense_id : rec_id },
	        success:function(data, textStatus, jqXHR)
	        {
				loading.remove();

	        	if (data!='null')
				{
				 	$("[name=expensesFORM_updateID]").val(data.expense_id);
					$('[name=template_id]').val(data.expense_template_id);
					$('[name=cost]').val(data.cost);
					$('[name=daterec]').val(data.daterec);
					$('[name=comments]').val(data.comments);
					$('[name=pay_method]').val(data.pay_method);

				 	$('#lblTitle_EXPENSES').html("Edit Expense");
					$('#modalEXPENSES').modal('toggle');
				}
				else
					alert("ERROR - Cant read the record.");
	        },
	        error: function(jqXHR, textStatus, errorThrown)
	        {
	        	loading.remove();
	            alert("ERROR");
	        }
	    });
	}

	function twoDigits(d) {
	    if(0 <= d && d < 10) return "0" + d.toString();
	    if(-10 < d && d < 0) return "-0" + (-1*d).toString();
	    return d.toString();
	}

	function date_now4mysql()
	{
		var d = new Date();
		var str_date = twoDigits(d.getDate()) + "-" + twoDigits(d.getMonth() + 1) + "-" + d.getFullYear();
		return str_date;
	}

	function getLastDateOfMonth(Year,Month){
 		var d = new Date((new Date(Year, Month+1,1))-1);

		var str_date = twoDigits(d.getDate()) + "-" + twoDigits(d.getMonth() + 1) + "-" + d.getFullYear();
		return str_date; 		
	}

	[settings](settings.php)

	<table id="expenses_tbl" data-striped="true">

		<thead>
			<tr>
				<th data-field="expense_template_id" data-visible="false">
					template_id
				</th>

				<th data-field="category" data-sortable="true">
					Category
				</th>

				<th data-field="jan" data-sortable="true">
					January
				</th>

				<th data-field="feb" data-sortable="true">
					February
				</th>

				<th data-field="march" data-sortable="true">
					March
				</th>

				<th data-field="april" data-sortable="true">
					April
				</th>

				<th data-field="may" data-sortable="true">
					May
				</th>

				<th data-field="june" data-sortable="true">
					June
				</th>

				<th data-field="july" data-sortable="true">
					July
				</th>

				<th data-field="aug" data-sortable="true">
					August
				</th>

				<th data-field="sept" data-sortable="true">
					September
				</th>

				<th data-field="oct" data-sortable="true">
					October
				</th>

				<th data-field="nov" data-sortable="true">
					November
				</th>

				<th data-field="dec" data-sortable="true">
					December
				</th>

			</tr>
		</thead>

		<tbody id="exp_rows"></tbody>
	</table>

<div class="modal fade" id="modalEXPENSES" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
	<div class="modal-dialog">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal" aria-hidden="true">
					×
				</button>

#### New

			</div>
			<div class="modal-body">
				<form id="formEXPENSES" role="form" method="post" action="save.php">

				<div class='form-group'>
					<label>Cost :</label>
					<input name='cost' class='form-control' placeholder='cost'>
				</div>

				<div class='form-group'>
					<label>Method :</label>
					<select name='pay_method' class='form-control'>
					</select>
				</div>

				<div class='form-group'>
					<label>Date :</label>  

					<input type="text" name="daterec" class="form-control" data-date-format="dd-mm-yyyy" readonly="" class="form_datetime">
				</div>

				<div class='form-group'>
					<label>Comments :</label>
					<input name='comments' class='form-control' maxlength="150" placeholder='comments'>
				</div>

				<input name="template_id" id="template_id" class="form-control" style="display: none;">
				<input name="expensesFORM_updateID" id="expensesFORM_updateID" class="form-control" style="display: none;">

				<div class="modal-footer">
					<button id="bntCancel_EXPENSES" type="button" class="btn btn-default" data-dismiss="modal">
						cancel
					</button>
					<button id="bntSave_EXPENSES" class="btn btn-primary" type="submit" name="submit">
						save
					</button>
				</div>
                </form>
            </div>
        </div>
    </div>
</div>

```

![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap383.png "snap383")

**the save.php :**
```js
//save.php
<?php session_start();="" if="" (!isset($_session["u"]))="" {="" echo="" json_encode(null);="" exit="" ;="" }="" else="" if($_session['level']="" !="-1){" die("you="" are="" not="" authorized="" to="" view="" this!");="" }="" if="" (!isset($_post['template_id'])="" ||="" !isset($_post['cost'])="" ||="" !isset($_post['daterec'])="" ||="" !isset($_post['pay_method'])="" ){="" echo="" "error010101010";="" return;="" }="" db="" require_once="" ('config.php');="" $db="connect();" $daterec="null;" if="" (!empty($_post['daterec']))="" {="" $dt="DateTime::createFromFormat('d-m-Y'," $_post['daterec']);="" $daterec="$dt-"?>format('Y-m-d');
}

if(isset($_POST['expensesFORM_updateID']) && !empty($_POST['expensesFORM_updateID']))
{
	$sql = "UPDATE expenses set expense_template_id=:expense_template_id, cost=:cost, daterec=:daterec, comments=:comments, owner_id=:owner_id, pay_method=:pay_method where expense_id=:expense_id";
	$stmt = $db->prepare($sql);
	$stmt->bindValue(':expense_id' , $_POST['expensesFORM_updateID']);
}
else
{

	$sql = "INSERT INTO expenses (expense_template_id, cost, daterec, comments, owner_id, pay_method) VALUES (:expense_template_id, :cost, :daterec, :comments, :owner_id, :pay_method)";
	$stmt = $db->prepare($sql);
}

$stmt->bindValue(':expense_template_id' , $_POST['template_id']);
$stmt->bindValue(':cost' , $_POST['cost']);
$stmt->bindValue(':daterec' , $daterec);
$stmt->bindValue(':comments' , $_POST['comments']);
$stmt->bindValue(':owner_id' , $_SESSION['id']);
$stmt->bindValue(':pay_method' ,  $_POST['pay_method']);

$stmt->execute();

echo $stmt->errorCode(); 
?>
```

**the fetch.php :**
```js
//fetch.php
<?php session_start();="" if="" (!isset($_session["u"])="" ||="" empty($_post['expense_id']))="" {="" echo="" json_encode(null);="" exit="" ;="" }="" else="" if($_session['level']="" !="-1){" die("you="" are="" not="" authorized="" to="" view="" this!");="" }="" try="" {="" include="" ('config.php');="" $db="connect();" $r="getRow($db," "select="" expense_id,="" expense_template_id,="" cost,="" date_format(daterec,'%d-%m-%y')="" as="" daterec,="" comments,="" owner_id,="" pay_method="" from="" expenses="" where="" expense_id="?" ,"="" array($_post['expense_id']));="" unicode="" header("content-type:="" application/json",="" true);="" echo="" json_encode($r);="" }="" catch="" (exception="" $e)="" {="" echo="" json_encode(null);="" }=""?>
```

origin - http://www.pipiscrew.com/?p=2187 php-year-expenses-organizer