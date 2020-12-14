---
title: setup gmail or gmail corporate to mail client
author: PipisCrew
date: 2018-10-13
categories: [news]
toc: true
---

<span style="color: #ff0000;">**Gmail Account Settings for IMAP**</span>
Incoming Server:<span style="color: #993366;"> imap.googlemail.com</span>
Port: 993
User Name: [youraccount]@gmail.com
Connection Security: SSL/TLS
Authentication: Password

<span style="color: #ff0000;">**Gmail Account Settings for POP**</span>
Incoming Server: <span style="color: #993366;">pop.gmail.com</span>
Port: 995
User Name: [youraccount]@gmail.com
Connection Security: SSL/TLS
Authentication: Password

**Outgoing Server**
Server Name: <span style="color: #993366;">smtp.googlemail.com</span>
Port: 465
User Name: [youraccount]@gmail.com
Authentication: Password
Connection Security: SSL/TLS

source - [http://support.google.com/mail/topic/3398031](http://support.google.com/mail/topic/3398031)

****ps

[ALERT] Please log in via your web browser: https://support.google.com/mail/accounts/answer/78754 (Failure)

goto & turr ON : [https://www.google.com/settings/security/lesssecureapps](https://www.google.com/settings/security/lesssecureapps) (source : https://support.google.com/accounts/answer/6010255)

* * *

<span style="color: #ff0000;">**Outlook/Hotmail/Live Incoming Mail (IMAP) Server**</span>
Server - imap-mail.outlook.com
Port - 993
Requires SSL - Yes  

<span style="color: #ff0000;">**Outlook/Hotmail/Live Outgoing  (SMTP)**</span>
Server - smtp-mail.outlook.com
Port - 25 (or 587/25 is blocked)
Authentication - Yes
Encrypted Connection - TLS

[for POP3 you have to enable it through Settings](https://support.office.com/en-us/article/pop-imap-and-smtp-settings-for-outlook-com-d088b986-291d-42b8-9564-9c414e2aa040)

* * *

## Commercial Office365

<span style="color: #ff0000;">**Outlook365 (IMAP) Server**</span>
Server - outlook.office365.com
Port - 993
Connection Security - SSL/TLS

<span style="color: #ff0000;">**Outlook/Hotmail/Live Outgoing  (SMTP)**</span>
Server - smtp.office365.com
Port 587, requires TLS if available; in Mozilla Thunderbird, choose "STARTTLS"
Authentication - Yes
Encrypted Connection - TLS

* * *

## Yahoo

<span style="color: #ff0000;">**Yahoo Incoming Mail (IMAP) Server**</span>

Server - imap.mail.yahoo.com
Port - 993
Requires SSL - Yes
Outgoing Mail (SMTP) Server

warning you have to go at Settings > Account Info > Account Security > Allow apps that use less secure sign in
turn it ON.

how to setup POP3 - https://help.yahoo.com/kb/SLN4724.html

**<span style="color: #ff0000;">Yahoo Outgoing (SMTP)</span>**

Server - smtp.mail.yahoo.com
Port - 465 or 587
Requires SSL - Yes
Requires authentication - Yes
Your login info

Email address - Your full email address (name@domain.com)
Password - Your account's password
Requires authentication - Yes

origin - http://www.pipiscrew.com/?p=2580 setup-gmail-or-gmail-corporate-to-mail-client