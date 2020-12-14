---
title: o[javascript] jQuery Datepicker
author: PipisCrew
date: 2014-12-02
categories: []
toc: true
---

A jQuery plugin that attaches a popup calendar to your input fields or shows an inline calendar for selecting individual dates or date ranges.

[http://keith-wood.name/datepick.HTML](http://keith-wood.name/datepick.HTML)

[javascript]

$(function() {
	 $('#dtpicker').calendarsPicker({
	 		dateFormat: "dd/mm/yyyy",
	 		minDate: +1,
	 		maxDate: +90,
	 });

	});//jQuery Ends

    <input id="dtpicker" placeholder="Arrival Date" required="">

[/javascript]

on form submit when txt_date is dd/mm/yyyy
[javascript]
var p_date = $('#txt_date').val().trim();
if (p_date.length != 10 || p_date.substring(2,3)!="/" || p_date.substring(5,6)!="/") {
	alert("Please enter date!");
	return;
}
else {
	var dtp_d = p_date.substring(0,2);
	var dtp_m = p_date.substring(3,5);
	var dtp_y = p_date.substring(6,10);

	var date_verify = new Date(dtp_m + "/" + dtp_d + "/" + dtp_y);
	//http://stackoverflow.com/a/10589791 || http://keith-wood.name/datepick.HTML#validate
	if (!date_verify instanceof Date && !isNaN(date_verify.valueOf()))
	{
		alert("Please enter a valid date!");
		return;
	}
}
[/javascript]

origin - http://www.pipiscrew.com/?p=2027 javascript-jquery-datepicker