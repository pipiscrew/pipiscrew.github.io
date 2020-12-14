---
title: o[js+bootstrap+php] send mail template
author: PipisCrew
date: 2017-02-09
categories: [js,bootstrap,php]
toc: true
---

```js

function sendmail2eventreg(e){
	e.preventDefault();
	$("#mail_recipient").val($("[name=email]").val());

	$('#modaloMAIL').modal('toggle');
}

$(function ()
	////////////////////////////////////////
	// MODAL SUBMIT aka save button
	$('#formoMAIL').submit(function(e) {
		e.preventDefault();

		loading.appendTo($('#formoMAIL'));

		var postData = $(this).serializeArray();
		var formURL = $(this).attr("action");

		$.ajax(
		{
			url : formURL,
			type: "POST",
			data : postData,
			success:function(data, textStatus, jqXHR) 
			{
				loading.remove();

				if (data==1)
					alert("Email successfully delivered to " + $("#mail_recipient").val());
				else
					alert("Error, please verify mail and retry!");

				$('#modaloMAIL').modal('toggle');
			},
			error: function(jqXHR, textStatus, errorThrown) 
			{
				alert("Server Error");      
			}
		});
	});

}); //jQ ends

<button onclick="sendmail2eventreg(event)" class="btn btn-success btn-sm  pull-right">Send Mail</button>

<div class='form-group'>
	<label>Email :</label>
	<input name='email' class='form-control' placeholder='email'>
</div>

<div class="modal fade bs-modal-lg" id="modaloMAIL" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
	<div class="modal-dialog modal-lg">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal" aria-hidden="true">
					×
				</button>

#### Send Proposal

			</div>
			<div class="modal-body">

				<form id="formoMAIL" role="form" method="post" action="send_mail.php">

						<div class='form-group'>
							<label>Recipient (multiple addresses separated by semicolon) :</label>
							<input id='mail_recipient' name='mail_recipient' class='form-control' placeholder='Recipient' required autofocus>
						</div>

						<div class='form-group'>
							<label>Subject :</label>
							<input id='mail_subject' name='mail_subject' class='form-control' placeholder='Subject' required autofocus>
						</div>

							<input id='mail_body' name='mail_body' data-role="none" class='editor'>

						<div class="modal-footer">
							<button id="bntCancel_MAIL" type="button" class="btn btn-default" data-dismiss="modal">
								cancel
							</button>
							<button id="bntSend_MAIL" class="btn btn-primary" type="submit" name="submit">
								send
							</button>
						</div>

				</form>
			</div>
		</div>
	</div>
</div>

```

```js
//send.php
<?php
@session_start();

if (!isset($_SESSION["id"])) {
	header("Location: login.php");
	exit ;
}

if (!isset($_POST["mail_recipient"]) || !isset($_POST["mail_subject"]) || !isset($_POST["mail_body"]) )
	die("required field(s) missing");

echo sendMail($_POST["mail_recipient"],$_POST["mail_subject"],$_POST["mail_body"]);

function sendMail($recipient_mail, $subject, $body)
{
	$headers = "From: x@x.com\r\n";
	$headers .= "MIME-Version: 1.0\r\n";
	$headers .= "Content-Type: text/html; charset=utf-8\r\n";

	$message = '';
	$message .= $body;
	$message .= '';

	// line with trick - http://www.xpertdeveloper.com/2013/05/set-unicode-character-in-email-subject-php/
	$updated_subject = "=?UTF-8?B?" . base64_encode($subject) . "?=";

    if (mail($recipient_mail, $updated_subject, $message, $headers)) {
      return true;
    } else {
      return false;
    }
}
```

### Using SMTP settings

Include on the top of PHP file

```js
//http://stackoverflow.com/a/6094059

ini_set('SMTP', 'smtp.x.com'); 
ini_set('smtp_port', 25); //default port for SMTP 
```

origin - http://www.pipiscrew.com/?p=1762 jsbootstrapphp-send-mail-template