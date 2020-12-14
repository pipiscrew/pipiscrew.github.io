---
title: Manipulate Calendar through Google API
author: PipisCrew
date: 2015-05-08
categories: []
toc: true
---

references 
Display the contents of a Google Calendar with PHP - [http://www.spunmonkey.com/display-contents-google-calendar-php/](http://www.spunmonkey.com/display-contents-google-calendar-php/)
Accessing Google Calendar with PHP - [http://www.daimto.com/accessing-google-calendar-with-php-oauth2/](http://www.daimto.com/accessing-google-calendar-with-php-oauth2/)

first make the setup at google console as described at (+ enable Calendar API) :
[https://www.pipiscrew.com/2015/04/php-send-mail-through-gmail-api/](https://www.pipiscrew.com/2015/04/php-send-mail-through-gmail-api/)

# list calendars

```js
//list calendars
<?php session_start();="" require_once="" 'google/autoload.php';="" or="" wherever="" autoload.php="" is="" located="" $client="new" google_client();="" $client-=""?>setClientId("x-x.apps.googleusercontent.com");
    $client->setClientSecret("xyxyxyxyxy");
    $client->setRedirectUri("https://x.com/pipis2/");
	$client->setAccessType('offline');
	$client->setApprovalPrompt('force');

	$client->addScope("https://mail.google.com/");
	$client->addScope("https://www.googleapis.com/auth/gmail.compose");
	$client->addScope("https://www.googleapis.com/auth/gmail.modify");
	$client->addScope("https://www.googleapis.com/auth/gmail.readonly");

	//calendar
	$client->addScope('https://www.googleapis.com/auth/calendar');

if (isset($_REQUEST['code'])) {
	//land here where user authenticated
	$code = $_REQUEST['code'];
	$client->authenticate($code);

	$_SESSION['gmail_access_token'] = $client->getAccessToken();

//	echo $_SESSION['gmail_access_token'];
//	exit;
	header("Location: https://x.com/pipis2/");
}

if (isset($_SESSION['gmail_access_token']) && !empty($_SESSION['gmail_access_token']) ) {
	//gmail_access_token setted;

    $client->setAccessToken($_SESSION['gmail_access_token']);    

	$service = new Google_Service_Calendar($client);    

	$calendarList  = $service->calendarList->listCalendarList();

	//lists user Calendar Names with their properties (not the events)
	echo '

' . print_r( $calendarList,1) . '
';

	while(true) {
		foreach ($calendarList->getItems() as $calendarListEntry) {
			//lists user calendar names (not the events)
			echo "009".$calendarListEntry->getSummary()."  
\n";
		}
		$pageToken = $calendarList->getNextPageToken();
		if ($pageToken) {
			$optParams = array('pageToken' => $pageToken);
			$calendarList = $service->calendarList->listCalendarList($optParams);
		} else {
			break;
		}
	}

}
else {
    // Failed Authentication
    if (isset($_REQUEST['error'])) {
        //header('Location: ./index.php?error_code=1');
        echo "error auth";
    }
    else{
        // Redirects to google for User Authentication
        $authUrl = $client->createAuthUrl();
        header("Location: $authUrl");
    }
}
```

sample on calendar item^ :
![](https://www.pipiscrew.com/wp-content/uploads/2015/05/snap008.png "snap008")

# list events of primary calendar

```js
<?php source="" http://developers.google.com/google-apps/calendar/quickstart/php#step_3_set_up_the_sample="" list="" events="" of="" primary="" calendar="" session_start();="" require_once="" 'google/autoload.php';="" or="" wherever="" autoload.php="" is="" located="" $client="new" google_client();="" $client-=""?>setClientId("x-x.apps.googleusercontent.com");
    $client->setClientSecret("xyxyxyxyxy");
    $client->setRedirectUri("https://x.com/pipis2/");
	$client->setAccessType('offline');
	$client->setApprovalPrompt('force');

	$client->addScope("https://mail.google.com/");
	$client->addScope("https://www.googleapis.com/auth/gmail.compose");
	$client->addScope("https://www.googleapis.com/auth/gmail.modify");
	$client->addScope("https://www.googleapis.com/auth/gmail.readonly");

	//calendar
	$client->addScope('https://www.googleapis.com/auth/calendar');

if (isset($_REQUEST['code'])) {
	//land here where user authenticated
	$code = $_REQUEST['code'];
	$client->authenticate($code);

	$_SESSION['gmail_access_token'] = $client->getAccessToken();

//	echo $_SESSION['gmail_access_token'];
//	exit;
	header("Location: https://x.com/pipis2/");
}

if (isset($_SESSION['gmail_access_token']) && !empty($_SESSION['gmail_access_token']) ) {
	//gmail_access_token setted;

    $client->setAccessToken($_SESSION['gmail_access_token']);    

	$service = new Google_Service_Calendar($client);    

	// Print the next 10 events on the user's calendar.
	$calendarId = 'primary';
	$optParams = array(
	  'maxResults' => 10,
	  'orderBy' => 'startTime',
	  'singleEvents' => TRUE,
	  'timeMin' => date('c'),
	);
	$results = $service->events->listEvents($calendarId, $optParams);

	if (count($results->getItems()) == 0) {
	  print "No upcoming events found.\n";
	} else {
	  print "Upcoming events:\n";
	  foreach ($results->getItems() as $event) {
		$start = $event->start->dateTime;
		if (empty($start)) {
		  $start = $event->start->date;
		}
		printf("%s (%s)\n", $event->getSummary(), $start);
	  }
	}

}
else {
    // Failed Authentication
    if (isset($_REQUEST['error'])) {
        //header('Location: ./index.php?error_code=1');
        echo "error auth";
    }
    else{
        // Redirects to google for User Authentication
        $authUrl = $client->createAuthUrl();
        header("Location: $authUrl");
    }
}
```

sample on event item^ :
![](https://www.pipiscrew.com/wp-content/uploads/2015/05/snap010.png "snap010")

# insert event to primary calendar

```js
<?php source="" http://developers.google.com/google-apps/calendar/v3/reference/events/insert="" list="" events="" of="" primary="" calendar="" session_start();="" require_once="" 'google/autoload.php';="" or="" wherever="" autoload.php="" is="" located="" $client="new" google_client();="" $client-=""?>setClientId("x-x.apps.googleusercontent.com");
    $client->setClientSecret("xyxyxyxyxy");
    $client->setRedirectUri("https://x.com/pipis2/");
	$client->setAccessType('offline');
	$client->setApprovalPrompt('force');

	$client->addScope("https://mail.google.com/");
	$client->addScope("https://www.googleapis.com/auth/gmail.compose");
	$client->addScope("https://www.googleapis.com/auth/gmail.modify");
	$client->addScope("https://www.googleapis.com/auth/gmail.readonly");

	//calendar
	$client->addScope('https://www.googleapis.com/auth/calendar');

if (isset($_REQUEST['code'])) {
	//land here where user authenticated
	$code = $_REQUEST['code'];
	$client->authenticate($code);

	$_SESSION['gmail_access_token'] = $client->getAccessToken();

//	echo $_SESSION['gmail_access_token'];
//	exit;
	header("Location: https://x.com/pipis2/");
}

if (isset($_SESSION['gmail_access_token']) && !empty($_SESSION['gmail_access_token']) ) {
	//gmail_access_token setted;

	$client->setAccessToken($_SESSION['gmail_access_token']); 	
	$service = new Google_Service_Calendar($client);    

	$event = new Google_Service_Calendar_Event();
	$event->setSummary('Costas Event');
	$event->setLocation('sandtron');
	$start = new Google_Service_Calendar_EventDateTime();
	$start->setDateTime('2015-05-08T14:00:00.000+03:00');
	$event->setStart($start);
	$end = new Google_Service_Calendar_EventDateTime();
	$end->setDateTime('2015-05-08T15:25:00.000+03:00');
	$event->setEnd($end);
	$attendee1 = new Google_Service_Calendar_EventAttendee();
	$attendee1->setEmail('group@pipiscrew.com');

	$attendees = array($attendee1);
	$event->attendees = $attendees;
	$createdEvent = $service->events->insert('primary', $event);

	echo $createdEvent->getId(); //print out the record id

}
else {
    // Failed Authentication
    if (isset($_REQUEST['error'])) {
        //header('Location: ./index.php?error_code=1');
        echo "error auth";
    }
    else{
        // Redirects to google for User Authentication
        $authUrl = $client->createAuthUrl();
        header("Location: $authUrl");
    }
}
```

# update event to primary calendar

```js
<?php source="" http://developers.google.com/google-apps/calendar/v3/reference/events/update="" update="" event="" of="" primary="" calendar="" session_start();="" require_once="" 'google/autoload.php';="" or="" wherever="" autoload.php="" is="" located="" $client="new" google_client();="" $client-=""?>setClientId("x-x.apps.googleusercontent.com");
    $client->setClientSecret("xyxyxyxyxy");
    $client->setRedirectUri("https://x.com/pipis2/");
	$client->setAccessType('offline');
	$client->setApprovalPrompt('force');

	$client->addScope("https://mail.google.com/");
	$client->addScope("https://www.googleapis.com/auth/gmail.compose");
	$client->addScope("https://www.googleapis.com/auth/gmail.modify");
	$client->addScope("https://www.googleapis.com/auth/gmail.readonly");

	//calendar
	$client->addScope('https://www.googleapis.com/auth/calendar');

if (isset($_REQUEST['code'])) {
	//land here where user authenticated
	$code = $_REQUEST['code'];
	$client->authenticate($code);

	$_SESSION['gmail_access_token'] = $client->getAccessToken();

//	echo $_SESSION['gmail_access_token'];
//	exit;
	header("Location: https://x.com/pipis2/");
}

if (isset($_SESSION['gmail_access_token']) && !empty($_SESSION['gmail_access_token']) ) {
	//gmail_access_token setted;
 	$client->setAccessToken($_SESSION['gmail_access_token']);    

 	$service = new Google_Service_Calendar($client);    

 	// First retrieve the event from the API.
	$event = $service->events->get('primary', '99proqddb6gb6'); //here 99proqddb6gb6 is the eventID got by an event

	////////////////////////////update start+end time
	$start = new Google_Service_Calendar_EventDateTime();
	$start->setDateTime('2015-05-08T14:00:00.000+03:00');
	$event->setStart($start);
	$end = new Google_Service_Calendar_EventDateTime();
	$end->setDateTime('2015-05-08T15:25:00.000+03:00');
	$event->setEnd($end);
	////////////////////////////update start+end time

	//update summary
	$event->setSummary('Appointment at Somewhere with Costas');

	//update @ google
	$updatedEvent = $service->events->update('primary', $event->getId(), $event);

	// Print the updated date.
	echo $updatedEvent->getUpdated();
}
else {
    // Failed Authentication
    if (isset($_REQUEST['error'])) {
        //header('Location: ./index.php?error_code=1');
        echo "error auth";
    }
    else{
        // Redirects to google for User Authentication
        $authUrl = $client->createAuthUrl();
        header("Location: $authUrl");
    }
}
```

origin - http://www.pipiscrew.com/?p=2972 php-manipulate-calendar-through-google-api