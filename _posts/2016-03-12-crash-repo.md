---
title: crash reporting with ACRA and MAB-LAB
author: PipisCrew
date: 2016-03-12
categories: [Uncategorized]
toc: true
---

**references :**
[ http://acra.ch/](http://acra.ch/)
[ https://github.com/ACRA/acra/wiki/Backends](https://github.com/ACRA/acra/wiki/Backends)

[https://github.com/Medialoha/MAB-LAB](https://github.com/Medialoha/MAB-LAB)
[ http://medialoha.net/](http://medialoha.net/)

<span style="color: #ff0000;">**ACRA :** </span>Catches exceptions, retrieves lots of context data and send them to the backend of your choice.

<span style="color: #0000ff;">**MAB-LAB :** </span>Backend for PHP with MYSQL (following instruction made when **v1.3.1-Helen #7** is the latest version)

MAB-LAB has installation instructions [http://medialoha.net/index.php/en/menu-mablab-en/menu-mabl-install](http://medialoha.net/index.php/en/menu-mablab-en/menu-mabl-install) , I wrote also this quick-text guide

1-
implement the ACRA exception handler to your application as described at http://acra.ch/

2-
download and upload the MAB-LAB backend to your server (dont forget to set permissions to 700)

3-
create a dbase for it, write down the credentials

4-
open 'includes\config.php' set the credentials, write down the tbl.prefix

5-
open 'install\db-install.sql' and replace all '%PREFIX%' with tbl.prefix setted on 'config.php'

6-
login to phpMySQL and execute 'install\db-install.sql'

7-
execute once the 'install\install.php'

8-
browse at http://domain.com/MABLABdirectory/index.php
username: admin
password: password

9-
goto Admin tools > Report Authentication uncheck if checked the 'Enable HTTP basic auth', btw you can enable also the email alert

10-
on android modify the @ReportsCrashes attribute (from step 1) to

```js
@ReportsCrashes (
formKey = "", // This is required for backward compatibility but not used
formUri = "http://domain.com/MABLABdirectory/report/report.php",
reportType = org.acra.sender.HttpSender.Type.JSON)
```

then when crash occurred, you have a view like :

[![](https://www.pipiscrew.com/wp-content/uploads/2014/02/snap880.png "snap880")](https://www.pipiscrew.com/wp-content/uploads/2014/02/snap880.png)

* * *

## Gathering Crash-reports and User-feedback for Your Android App

last JAR is v4.6.2, then only AAR

[https://blog.higgsboson.tk/2014/06/10/gathering-crash-reports-and-user-feedback-for-your-android-app/](https://blog.higgsboson.tk/2014/06/10/gathering-crash-reports-and-user-feedback-for-your-android-app/)

origin - http://www.pipiscrew.com/?p=887 android-crash-reporting-with-acra-and-mab-lab