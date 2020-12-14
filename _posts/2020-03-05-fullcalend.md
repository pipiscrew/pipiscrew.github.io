---
title: fullcalendar example
author: PipisCrew
date: 2020-03-05
categories: [js,php]
toc: true
---

the full example, can be found at :
https://github.com/pipiscrew/fullcalendar-php-example

* * *

When is not logged-in, view full calendar, with read only permissions.
![fcalendar2](https://www.pipiscrew.com/wp-content/uploads/2016/09/fcalendar2.jpg)

this is the view of admin
![fcalendar1](https://www.pipiscrew.com/wp-content/uploads/2016/09/fcalendar1.jpg)

introduction : 
the application runs in index.php, all workers are available to view the calendar. When user logged-in (login.php) has the point3 - point2 - at point4 can move the event(s).

point1 - anchor drives to login.php / when logged-in drivers to logout.php
point2 - lists the workers, added from point3 (saved to local sqlite)

* * *

I will not explain the login/logout already done, on previous articles. We will focus, on security and how manipulate the fullcalendar.js aka https://fullcalendar.io/

all the php scripts, contains as header :
```js
<?php $is_admin="false;" @session_start();="" if="" (isset($_session["id"]))="" {="" date_default_timezone_set("utc");="" if="" ($_session["login_expiration"]="" !="date("Y-m-d"))" {="" session_destroy();="" header("location:="" login.php");="" exit="" ;="" }="" else="" {="" $is_admin="true;" }="" }=""?>

```

index.php - references
```js

 <!-- needed for drag&drop (customized download at official site final size 72kb)
```

the calendar html is as the following :
```js
			<div class="row">
				<div class="col-md-12">
					<div class="panel">
						<div class="panel-heading">
							<div class="panel-title">

#### CALENDAR

</div>
						</div> 
						<div class="panel-body">
							<div class="row">
								<?php if($is_admin){ ?>
									<div class="col-md-3">
										<div id="external-events">
											<div class="legend">Create Event</div>

											<form action="add_user.php" id="create-event">
												<div class="input-group">
													<div class="inputer">
														<div class="input-wrapper">
															<input id="event-title" name="event-title" type="text" class="form-control">
														</div>
													</div>
													<div class="input-group-btn">
														<button id="add-event" type="submit" class="btn btn-flat btn-default">Add</button>
													</div> 
												</div> 
											</form>

											<div class="legend">Draggable Events</div>
											<div class="draggable-events">
												<?php 
												include 'config.php';

												$db = connect();

												$r = getSet($db,"select * from users order by user_mail", null);

												$elements = "";
												foreach($r as $row){
													if(strpos($row["user_mail"], '@') == FALSE )
													echo "<div class=\"fc-event\" data-userid=\"{$row["user_id"]}\"><span>{$row["user_mail"]}</span> <button type=\"button\" class=\"close\">×</button></div>\r\n";
												}
												?>
											</div> 
											<p>
												<input type="checkbox" id="drop-remove" checked/>
												<label for="drop-remove">Remove After Drop</label>
											</p>
											<p>
												<input type="checkbox" id="drop-type"/>
												<label for="drop-type">Add as day off</label>
											</p>
										</div> 
									</div> 
									<div class="col-md-9">
									<?php } else{  ?>
										<div class="col-md-12">
									<?php }?>

											<div id="calendar"></div> 
										</div> 
									</div> 
							</div> 
						</div> 
					</div> 
				</div> 
			</div> 
		</div> 

		<div id="modaloSUBSECTOR" class="modal fade bs-example-modal-sm" tabindex="-1" role="dialog" aria-labelledby="mySmallModalLabel" aria-hidden="true">
			<div class="modal-dialog modal-sm">
				<div class="modal-content">

					<div class="modal-header">

						<button type="button" class="close" data-dismiss="modal"><span aria-hidden="true">×</span><span class="sr-only">Close</span></button>

#### Please choose type 

					</div>
					<div class="modal-body">
						<button type="button" id="btn_dayoff_type" data-eventid="1" class="btn btn-purple btn-block btn-ripple">home office</button>
						<button type="button" id="btn_dayoff_type" data-eventid="2" class="btn btn-blue btn-block btn-ripple">vacation</button>
						<button type="button" id="btn_dayoff_type" data-eventid="3" class="btn btn-teal btn-block btn-ripple">half-day vacation</button>
						<button type="button" id="btn_dayoff_type" data-eventid="4" class="btn btn-deep-orange btn-block btn-ripple">left</button>
						<button type="button" id="btn_dayoff_type" data-eventid="5" class="btn btn-success btn-block btn-ripple">compensate</button>
						<button type="button" id="btn_dayoff_type" data-eventid="6" class="btn btn-yellow btn-block btn-ripple">sickness/doctor</button>
						<button type="button" id="btn_dayoff_type" data-eventid="7" class="btn btn-brown btn-block btn-ripple">training</button>
						<button type="button" id="btn_dayoff_type" data-eventid="8" class="btn btn-blue-grey btn-block btn-ripple">public holiday</button>
						<button type="button" id="btn_dayoff_type" data-eventid="9" class="btn btn-inverted btn-block btn-ripple">personal leave</button>

						<div class="input-group">
							<div class="inputer">
								<div class="input-wrapper">
									<input id="event_comment" name="event_comment" type="text" class="form-control">
								</div>
							</div>
						</div> 
					</div>
				</div><!-- /.modal-content -->
			<!-- /.modal-dialog -->

```

Line 09 = if admin logged-in make the drag&drop area visible, make a DB connection enumerate the users.
Line 39 = when enumerating the users, add HTML5 attribute (userid) to each div, will be used for dbase record.
Line 53 = when admin use ```jsclass="col-md-9"``` otherwise use ```jsclass="col-md-12"``` for calendar.
Line 68 = modal with dayoff type.
Line 79-87 = modal hardcoded buttons, represent the dayoff types. All has the same ID (btn_dayoff_type) and different HTML5 data attribute (eventid), will be used for dbase record.

* * *

the js has as :
```js
//js

origin - http://www.pipiscrew.com/?p=6127 js-fullcalendar-example