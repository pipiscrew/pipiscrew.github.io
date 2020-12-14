---
title: PHPMailer - Send mails using SMTP
author: PipisCrew
date: 2015-03-31
categories: []
toc: true
---

reference:
[http://github.com/PHPMailer/PHPMailer/blob/master/examples/gmail.phps](http://github.com/PHPMailer/PHPMailer/blob/master/examples/gmail.phps)

A full-featured email creation and transfer class for PHP
[http://github.com/PHPMailer/PHPMailer](http://github.com/PHPMailer/PHPMailer)

source : [http://asif18.com/7/php/send-mails-using-smtp-in-php-by-gmail-server-or-own-domain-server/](http://asif18.com/7/php/send-mails-using-smtp-in-php-by-gmail-server-or-own-domain-server/)
```js
<?php include="" "classes/class.phpmailer.php";="" include="" the="" class="" file="" name="" if(isset($_post["send"])){="" $email="$_POST["email"];" $mail="new" phpmailer;="" call="" the="" class="" $mail-=""?>IsSMTP(); 
    $mail->Host = SMTP_HOST; //Hostname of the mail server
    $mail->Port = SMTP_PORT; //Port of the SMTP like to be 25, 80, 465 or 587
    $mail->SMTPAuth = true; //Whether to use SMTP authentication
    $mail->Username = SMTP_UNAME; //Username for SMTP authentication any valid email created in your domain
    $mail->Password = SMTP_PWORD; //Password for SMTP authentication
    $mail->AddReplyTo("reply@yourdomain.com", "Reply name"); //reply-to address
    $mail->SetFrom("from@yourdomain.com", "x SMTP Mailer"); //From address of the mail
    // put your while loop here like below,
    $mail->Subject = "Your SMTP Mail"; //Subject od your mail
    $mail->AddAddress($email, "Asif18"); //To address who will receive this email
    $mail->MsgHTML("**Hi, your first SMTP mail has been received. Great Job!..   

by [Asif18](http://asif18.com)**");
    $mail->AddAttachment("images/asif18-logo.png"); //Attach a file here if any or comment this line, 
    $send = $mail->Send(); //Send the mails
    if($send){
        echo '<center>

### Mail sent successfully

</center>';
    }
    else{
        echo '<center>

### Mail error: 

</center>'.$mail->ErrorInfo;
    }
}
?>
```

origin - http://www.pipiscrew.com/?p=1845 php-send-mails-using-smtp