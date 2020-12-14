---
title: jQuery, using parent() to read the elements values
author: PipisCrew
date: 2016-04-27
categories: [js]
toc: true
---

![snap428](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap428.png)

```js
//test.html

	$(function() {
		$(".div_box").hover(
			   function () {
				   $(this).find(".trick-address").show();
			   },
			   function () {
				   $(this).find(".trick-address").hide();
			   }
		);

		$('.trick-address').click(function () {
			var parentDiv = $(this).parent().prev();

			console.log('CompanyName - ' + $(parentDiv).find("#CompanyName").html());
			console.log('CompanyActivity - ' + $(parentDiv).find("#CompanyActivity").html());
			console.log('TaxNumber - ' + $(parentDiv).find("#TaxNumber").html());
			console.log('TaxOffice - ' + $(parentDiv).find("#TaxOffice").html());
			console.log('Address - ' + $(parentDiv).find("#Address").html());
			console.log('PostCode - ' + $(parentDiv).find("#PostCode").html());
			console.log('Phone - ' + $(parentDiv).find("#Phone").html());
		});
	});

<style>
	.div_box {
		height: 120px;
		float: left;
		padding: 10px 10px 0 10px;
		background: #ebebeb;
		margin-right: 20px;
		position: relative;
		transition: all .2s;
		margin-top: 10px;
	}
	 .div_box:hover {
		cursor: pointer;
		background: #c4c3c3;
	}

	.trick-address {
		background: url("img/pencil.png") no-repeat 5px 6px #F3F3F3;
		height: 24px;
		margin-top: 0;
		position: absolute;
		right: 0;
		top: 0;
		width: 24px;
		display: none;
	}
</style>

	<div id="divdiv_box_1" class="div_box">
		<div class="test_address_detail_area">
				<div id="CompanyName" class="address_detail">testCompanyName1</div>
				<div id="CompanyActivity" class="address_detail">testCompanyActivity1</div>
				<div id="TaxNumber" class="address_detail">testTaxNumber1</div>
				<div id="TaxOffice" class="address_detail hidden">testTaxOffice1</div>
				<div id="Address" class="address_detail hidden">testAddress1</div>
				<div id="PostCode" class="address_detail hidden">testPostCode1</div>
				<div id="Phone" class="address_detail hidden">testPhone1</div>
		</div>
		<div class=""></div>
	</div>

	<div id="divdiv_box_2" class="div_box">
		<div class="test_address_detail_area">
				<div id="CompanyName" class="address_detail">testCompanyName2</div>
				<div id="CompanyActivity" class="address_detail">testCompanyActivity2</div>
				<div id="TaxNumber" class="address_detail">testTaxNumber2</div>
				<div id="TaxOffice" class="address_detail hidden">testTaxOffice2</div>
				<div id="Address" class="address_detail hidden">testAddress2</div>
				<div id="PostCode" class="address_detail hidden">testPostCode2</div>
				<div id="Phone" class="address_detail hidden">testPhone2</div>
		</div>
		<div class=""></div>
	</div>

```

origin - http://www.pipiscrew.com/?p=5138 jquery-using-parent-to-read-the-elements-values