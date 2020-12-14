---
title: FullCalendar (display appointments, saved from erp)
author: PipisCrew
date: 2016-09-24
categories: [Uncategorized]
toc: true
---

reference
[http://fullcalendar.io/](http://fullcalendar.io/)

Is a jQuery plugin that provides a full-sized, drag & drop event calendar like the one below. It uses AJAX to fetch events on-the-fly and is easily configured to use your own feed format. It is visually customizable with a rich API.

copy

*   fullcalendar.min.css

*   fullcalendar.print.css

*   moment.min.js

*   jquery.min.js

*   fullcalendar.min.js

```js
//main.php
<?php session_start();="" require_once="" ('config.php');="" $users_rows="null;" if(!isset($_session["u"])){="" header("location:="" login.php");="" exit="" ;="" }="" else="" if($_session['level']="" !="-89){" $db="connect();" $users_rows="getSet($db," "select="" *="" from="" users="" order="" by="" user_level_id",="" null);="" }=""?>

	$(document).ready(function() {

	///////////////////////////////////////////////////////////// FILL users
	var jArray_users =   <?php echo json_encode($users_rows); ?>;

	var combo_users_rows = "<option value='0'></option>";
	for (var i = 0; i < jArray_users.length; i++)
	{
		combo_users_rows += "<option value='" + jArray_users[i]["user_id"] + "'>" + jArray_users[i]["fullname"] + "</option>";
	}

	$("[name=user_id]").html(combo_users_rows);
	$("[name=user_id]").change(); //select row 0 - no conflict on POST validation @ PHP
	///////////////////////////////////////////////////////////// FILL users

//when combo change
		$('#user_id').change(function () {
			//http://stackoverflow.com/a/10229981
            var selectedSite = $(this).val();
            var events = {
				url: 'x.php',
				data: {
					user_id: $('#user_id').val()
				},
				error: function() {
					alert("error");
				}
            }
            $('#calendar').fullCalendar('removeEventSource', events);
            $('#calendar').fullCalendar('addEventSource', events);

		});

//instantiate calendar
		$('#calendar').fullCalendar({
			header: {
				left: 'prev,next today',
				center: 'title',
				right: 'month,agendaWeek,agendaDay'
			},
			defaultDate: '2015-01-01',
			editable: false,
			eventLimit: true, // allow "more" link when too many events
			events: {
				url: 'x.php',
				data: {
					user_id: $_SESSION['id']
				},
				error: function() {
					alert("error");
				}
			},
			loading: function(bool) {
				$('#loading').toggle(bool);
			},
		    eventClick: function(calEvent, jsEvent, view) {
				console.log(calEvent.id);
		      //  $(this).css('border-color', 'red');
		    }
		});

	});

<style>

	body {
		margin: 0;
		padding: 0;
		font-family: "Lucida Grande",Helvetica,Arial,Verdana,sans-serif;
		font-size: 14px;
	}

	#loading {
		display: none;
		position: absolute;
		top: 10px;
		right: 10px;
	}

	#calendar {
		max-width: 900px;
		margin: 40px auto;
		padding: 0 10px;
	}

</style>

	<div id='loading'>loading...</div>

	<select id="user_id" name="user_id"></select>

	<div id='calendar'></div>

```

//x.php
```js
//x.php
<?php require_once="" ('config.php');="" $db="connect();" create="" an="" array="" $record="array();" query="" for="" records="" $rows="getSet($db," select"="" client_appointment_id="" as="" id,client_name="" as="" title,client_appointment_datetime="" as="" start="" from="" client_appointments="" left="" join="" clients="" on="" clients.client_id="client_appointments.client_appointment_client_id" where="" client_appointment_owner_id=".$_GET[" user_id"]."="" and="" client_appointment_datetime="" between="" '".$_get["start"]."'="" and="" '".$_get["end"]."'",="" null);="" for="" each="" record="" foreach($rows="" as="" $row)="" {="" $datetime="new" datetime($row['start']);="" convert="" mysql="" datetime="" to="" iso8601="" format="" fullcalendar="" compatible="" $record[]="array(" id""="=""?"?> $row['id'],"title" => $row['title'],"start" => $datetime->format(DateTime::ISO8601));
	//add it to array
}

echo json_encode($record);
?>
```

PHP produces something like (response to line **main.html 51+75**) :
![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap391.png "snap391")

* * *

colorize the bars, when return json contains 'color' on each event
![](https://www.pipiscrew.com/wp-content/uploads/2015/01/snap394.png "snap394")

use **qtip** by FullCalendar [http://stackoverflow.com/a/21342695](http://stackoverflow.com/a/21342695)

**mouseevents** [http://stackoverflow.com/a/12466543](http://stackoverflow.com/a/12466543)

* * *

//read result
```js
	events: {
		url: 'x.php',
		data: {
			user_id: <?=$_session['id']???>
		},
		success :  function(e) {
			console.log(e); //returned json
		},
		error: function() {
			alert("error");
		}
	},
```

* * *

Change the cursor pointer when mouseover
[http://stackoverflow.com/a/25154123](http://stackoverflow.com/a/25154123)

```js
.fc-content {
    cursor: pointer;
}
```

origin - http://www.pipiscrew.com/?p=2215 js-fullcalendar