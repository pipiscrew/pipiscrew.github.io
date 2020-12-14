---
title: SQL Server 2014 - Import and Export Wizard
author: PipisCrew
date: 2016-01-14
categories: [sql]
toc: true
---

reference - [http://stackoverflow.com/a/29712653](http://stackoverflow.com/a/29712653)

Use the SQL Server Import and Export Wizard, and choose New... when choosing the destination database.

Right Click Database > Tasks > Import Data.

Choose a Data Source

Data Source: SQL Server Native Client
Server Name: the remote server
Authentication:
Database: the db name
Choose a Destination

Data Source: SQL Server Native Client
Server Name: the local server
Authentication:
Database: New...
The rest is straight forward.

Picture It!

![snap019](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap019.png)

![snap020](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap020.png)

![snap021](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap021.png)

![snap022](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap022.png)

![snap023](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap023.png)

![snap024](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap024.png)

origin - http://www.pipiscrew.com/?p=3207 sql-server-2014-import-and-export-wizard