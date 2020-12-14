---
title: o[bootstrap-table] a story w two tables and one modal
author: PipisCrew
date: 2014-10-22
categories: []
toc: true
---

reference [http://github.com/wenzhixin/bootstrap-table/](http://github.com/wenzhixin/bootstrap-table/)

The primary table :
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap103.png "snap103")

where the PHP on top is :
```js
<?php include="" db="" require_once="" ('config.php');="" $db="connect();" $contracts="null;" read="" contracts="" $contracts="getSet($db," select"="" offer_id,="" date_format(offer_date_rec,'%d-%m-%y="" %h:%i')="" as="" date_created,="" users.fullname="" as="" user,format(gen_total,2)="" as="" gen_total,date_format(invoice_when,'%d-%m-%y="" %h:%i')="" as="" invoice_when,usb.fullname="" as="" invoice_user,="" case="" offer_type="" when="" 1="" then="" 'new'="" when="" 2="" then="" 'update'="" when="" 3="" then="" 'renewal'="" else="" 'unknown'="" end="" as="" offer_type,ifnull(date_format(service_starts,'%d-%m-%y'),'no="" setted')="" as="" starts,="" ifnull(date_format(service_ends,'%d-%m-%y'),'no="" setted')="" as="" ends="" from="" offers="" left="" join="" users="" on="" users.user_id="offers.offer_seller_id" left="" join="" users="" as="" usb="" on="" usb.user_id="offers.invoice_user" where="" company_id="?" and="" is_paid="1" order="" by="" offer_date_rec="" desc",="" array($_get['id']));="" read="" contracts=""?>
```

the HTML is :
```js
			<table id="contracts_tbl" data-striped="true" data-click-to-select="true" data-single-select="true">
				<thead>
					<tr>
						<th data-field="state" data-checkbox="true"></th>
						<th data-field="id">ID</th> 
						<!--data-visible="false"-->
						<th data-field="col_descr" data-sortable="true">Created</th>
						<th data-sortable="true">Seller</th>
						<th data-sortable="true">Total Cost €</th>
						<th data-sortable="true">Type</th>
						<th data-sortable="true">Service Starts</th>
						<th data-sortable="true">Service Ends</th>
						<th data-sortable="true">Invoice</th>

					</tr>
				</thead>

				<tbody id="contracts_rows"></tbody>
			</table>
```

the JS is :
```js
					 ///////////////////////////////////////////////////////////// FILL Contracts grid
					 var jArray_contracts =   <?php echo="" json_encode($contracts);=""?>;

					 var combo_contracts_rows = "";
					 for (var i = 0; i < jarray_contracts.length;="" i++)="" {="" combo_contracts_rows="" +="<tr><td></td><td>" +="" jarray_contracts[i]["offer_id"]="" +=""><td>" + jArray_contracts[i]["date_created"] + "</td>" +
					 	"<td>" + jArray_contracts[i]["user"] + "</td><td>" + jArray_contracts[i]["gen_total"] + "</td><td>" + jArray_contracts[i]["offer_type"] + "</td>" +
					 	"<td>" + jArray_contracts[i]["Starts"] + "</td><td>" + jArray_contracts[i]["Ends"] + "</td>";

					 	if ( jArray_contracts[i]["invoice_when"]==null)
							combo_contracts_rows +=	"<td>[Download]()";
					 	else
					 	{//reactivate green button
					 	}

					 	combo_contracts_rows +="</td>";
					 }

					 $("#contracts_rows").html(combo_contracts_rows);
					 ///////////////////////////////////////////////////////////// FILL Contracts grid

					 //convert2magic!
					 $("#contracts_tbl").bootstrapTable();
```

focus on :
```js
combo_contracts_rows +=	"<td>[Download]()";
```
this one creates an anchor, onclick call the invoice_details_choose method parameterized by primary record ID^ (aka offer_id)

the invoice_details_choose () (out of jQuery era) :
```js
	 //when download button clicked from grid - refresh destinations (invoice details) on grid in modal!
	 //dynamic handler for grid buttons
	 function invoice_details_choose(offer_id)
	 {
		//store to modal hidden input, the offerID selected by primary grid!
		$("#CHOOSEINVOICE_offerID").val(offer_id);

			$.ajax(
				{
					url : 'x_get_invoices.php',
					dataType : 'json',
					type : 'POST',
					data :	{ "client_id" : <?= $_get['id']=""?>	}, //read client invoice details (aka branches)
					success : function(data)
					{
						//when response
						var r = data.recs;
						var tbl ="";

						if (r==undefined)
						{
							alert("error : no record");
							return;
						}					 						

						//construct table rows
						for (var i = 0; i < r.length;="" i++)="" {="" tbl="" +="<tr><td>" +="" r[i]["client_invoice_detail_id"]="" +=""></td><td>" + r[i]["company_name"] + "</td>" +
							"<td>" + r[i]["occupation"] + "</td><td>" + r[i]["city"] + "</td><td>" + r[i]["country_id"] + "</td><td>" + r[i]["vat_no"] + "</td><td>" + r[i]["tax_office_id"] + "</td>";
						}

						//set rows to table 
						$("#CHOOSEINVOICE_rows").html(tbl);

						//convert2magic!
						$("#CHOOSEINVOICE_tbl").bootstrapTable();

						//show modal
						$('#modalCHOOSEINVOICE').modal('toggle');
					},
					error : function(e)
					{
						alert("error");
					}
				});

			//location.reload(true);
		}
```

where the CHOOSEINVOICE_tbl in html setted on cardview by default in modalCHOOSEINVOICE :
```js

<div class="modal fade" id="modalCHOOSEINVOICE" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
	<div class="modal-dialog">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal" aria-hidden="true">
					×
				</button>

#### Please Choose Client Invoice Details

			</div>
			<div class="modal-body">
			           <!--data-striped=true-->				
					<table id="CHOOSEINVOICE_tbl" data-card-view="true" data-height="500">

							<thead>
								<tr>
									<th data-field="client_invoice_detail_id" data-visible="false">
										id
									</th>

									<th data-field="company_name" data-sortable="true">
										Company Name
									</th>

									<th data-field="occupation" data-sortable="true">
										Occupation
									</th>

									<th data-field="city" data-sortable="true">
										City
									</th>

									<th data-field="country_id" data-sortable="true">
										Country
									</th>

									<th data-field="vat_no" data-sortable="true">
										VAT
									</th>

									<th data-field="tax_office_id" data-sortable="true">
										Tax Office
									</th>

								</tr>
							</thead>
							 <tbody id="CHOOSEINVOICE_rows"></tbody>
						</table>

				<form id="formCHOOSEINVOICE" name="formCHOOSEINVOICE" role="form" method="post" action="generate_invoice.php">

						<input name="CHOOSEINVOICE_offerID" id="CHOOSEINVOICE_offerID" class="form-control" style="display:none;">
						<input name="CHOOSEINVOICE_invoicedetailID" id="CHOOSEINVOICE_invoicedetailID" class="form-control" style="display:none;">

						<div class="modal-footer">
							<button id="bntCancel_CHOOSEINVOICE" type="button" class="btn btn-primary" data-dismiss="modal">
								cancel
							</button>
						</div>
                </form>
            </div>
        </div>
    </div>
</div>

```

the modalCHOOSEINVOICE events are :
```js
				    ////////////////////////////////////////
				    // MODAL FUNCTIONALITIES [START]-invoice details
				    //when modal closed, hide the warning messages + reset
				    $('#modalCHOOSEINVOICE').on('hidden.bs.modal', function() {
				        //when close - clear elements
				        $('#formCHOOSEINVOICE').trigger("reset");

				        //destroy bootstrap-table
				        $("#CHOOSEINVOICE_tbl").bootstrapTable('destroy');
				    });

				    //functionality when the modal already shown and its long, when reloaded scroll to top
				    $('#modalCHOOSEINVOICE').on('shown.bs.modal', function() {
				        $(this).animate({
				            scrollTop : 0
				        }, 'slow');
				    });
				    // MODAL FUNCTIONALITIES [END]-invoice details
				    ////////////////////////////////////////
```

so when by primary table the download button clicked > the javascript function run > read the records by PHP > show as at bootstrap-table as card-view, we are here :
![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap104.png "snap104")

now when a row clicked, we using the bootstrap-table event **click-row.bs.table** as :
```js
	//when row clicked by bootstrap-table (card view)-there is no other way(?)
	$('#CHOOSEINVOICE_tbl').on('click-row.bs.table', function (e, row, $element)
	{
		console.log(row.client_invoice_detail_id);
		if (!confirm("Please confirm the invoice details will be :\r\n"+ row.company_name + "\r\n" + row.vat_no + "\r\n" + row.tax_office_id))
			return;

		//show an indicator
		loading.appendTo(document.body);

		//close modal
		$('#modalCHOOSEINVOICE').modal('toggle');

		//set selected to form input element
		$("#CHOOSEINVOICE_invoicedetailID").val(row.client_invoice_detail_id);

		//submit native the form!
		document.formCHOOSEINVOICE.submit();

		//go back after 5sec
		setTimeout(function(){
			window.location="x_details.php?showcontracts=1&id=<?= $_get['id']=""?>";
		}, 5000);						

	});
```

origin - http://www.pipiscrew.com/?p=1582 bootstrap-table-a-story-w-two-tables-and-one-modal