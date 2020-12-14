---
title: Send email using Office 365 account
author: PipisCrew
date: 2016-08-03
categories: [.net]
toc: true
---

```js
//source http://weblogs.asp.net/sreejukg/send-email-using-office-365-account-and-c
String userName = "user@domain.com";
String password = "your password";
MailMessage msg = new MailMessage();
msg.To.Add(new MailAddress("ToAddress"));
msg.From = new MailAddress(userName);
msg.Subject = "Test Office 365 Account";
msg.Body = "Testing email using Office 365 account.";
msg.IsBodyHtml = true;
SmtpClient client = new SmtpClient();
client.Host = "smtp.office365.com";
client.Credentials = new System.Net.NetworkCredential(userName, password);
client.Port = 587; 
client.EnableSsl = true;
client.Send(msg);
```

origin - http://www.pipiscrew.com/?p=5964 send-email-using-office-365-account