---
title: SQL Server 2008-14 Addons
author: PipisCrew
date: 2016-01-18
categories: [sql]
toc: true
---

SQL Formatter Add-In for SSMS

[https://ssmsaddins.codeplex.com/](https://ssmsaddins.codeplex.com/)

### Addin: DataScripter

This Addin for SQL Server Management Studio 2008 allows you to generate INSERT statements for all values of a table easily. Just select Script Data as from the context menu of the table and choose one of the options
INSERT: Insert statements without column names are generated
INSERT with column names: should by obvious ;-)

### Addin: ObjectFinder

Will perform a fulltext search over your Stored Procedures, Functions and Triggers. You can easily find a object that contains a string (e.g. a table name is referenced in a stored procedure) and open it's definition.

### Addin: Fulltext Manager for SQL Express

Will perform a fulltext search over your Stored Procedures, Functions and Triggers. You can easily find a object that contains a string (e.g. a table name is referenced in a stored procedure) and open it's definition.

* * *

similar - [http://www.ssmsboost.com/](http://www.ssmsboost.com/)

### Script object

Open source code of object located at cursor position in sql editor. Shortcut:[F2]
Equal to "Go To Definition" function in Visual Studio. Object script is opened in "well-named" tab, containing object name and other information (customizeable)	

### Locate object

Quickly find in object explorer object located at cursor position in sql editor. Shortcut: [Ctrl-F2]	

### Copy data from Results Grid to Excel

Right-click selected cells to copy. Numeric and Date/Time formats will be preserved when copying	

### Results Grid aggregates

SUM, AVG, MIN, MAX and COUNT aggregates are shown
for selected range of cells in Results Grid	

### Edit Top N Rows

Open table data editor directly from SQL Editor. Right-click the table and select "Open top N Rows". N is standard setting from SSMS preferences	

### Fatal actions guard

Protects you from running DML statements (UPDATE,DELETE) without WHERE clause. TRUNCATE TABLE is handled as well. Additionally you can define list of prohibited keywords. This feature saves you from fatal modifications on important databases	

### Preferred connections

-Connection aliases
-Connection coloring
-Active and passive protection of important databases by visual warning and blocking of critical DML without WHERE clause
-Fixed SSMS issue with "Additional connection parameters"
-Automatically connect object explorer on startup
-Automatically open empty script window on startup

### Quick Connections Switch

Drop-down on toolbar, allowing to switch connections between servers	

### Executed statements history

Keep track of executed SQL Statements, including additional information about execution context, result and duration	

### SQL Editor contents history

Keep snapsots of SQL Editor contents, while working on SQL Scripts. It is much better than built-in UNDO, as far as it is permanently saved on disk and can be opened anytime later	

### Recent Sessions

Autorecovery of recent sessions, including unsaved documents and their connections	

### Recent Tabs

autorecovery of recent tabs, including unsaved documents and their connections. Includes "Restore last closed tab" feature known from internet browsers	

### Recent connections

SSMSBoost keeps track of last databases/servers used and allows to reuse them. Recent connection can be promoted to Preferred connection	

### Format SQL Documents

Easily apply "good" format for your SQL source code. For maximum flexibility we have included 2 versions of SQL formatters: old good "Poor Man's T-SQL Formatter" (displayed as "Old styled formatting") and our own flexible multi-template SQL formatter.	

### Regions

You can re-use well-known syntax:
--#region [Name]
--#endregion
Start/End tokens can be customized to your team's needs	

### Vertical guidelines

Display one or more vertical lines in SQL Editor to keep length of your code lines under control	

### Quickly add database to preferred connections

Database node context menu command in Object Explorer	

### Set database as active connection

Database node context menu command in Object Explorer	

### Auto replacements

Auto-replacements in text editor	

### Find in Results Grid

Search for values in results grid using wildcards	

### ResultsGrid Visualizers

### 
Visualize any files saved in tables: Pictures, Office Documents, PDF Files, etc	

### ResultsGrid Scripter

Flexible Template-based Results Grid Scripting: define your own export format for results from grid	

### Copy Results Grid headers

Allows to copy column names from resulst grid directly (all or headers of selected cells)	

### Copy original cell contents

Copies strings and data from results grid preserving line breaks	

### Search for objects using wildcards

Search for objects across databases using wildcards	

### 1-click Comment/Uncomment selected SQL code using /**/ syntax

Show filename, server/database of current document in SSMS title - template is customizeable	

### Jump-Navigate through BEGIN/END blocks

Show filename, server/database of current document in SSMS title - template is customizeable	

### Track current database

Focus database note in Object Explorer, corresponding to current sql editor connection	

### Workspaces

Remember opened documents and their connections as named Workspace, re-open it anytime	

### Define macros

Define simple sequences of commands and assign shortcuts to them	

### Assign new keyboard shortcuts

Define/Re-Define keyboard shortcuts	

### Scripting options

Define scripting options used to script objects	

### Dump all SSMS commands and shortcuts

Outputs full list of commands registered in SSMS, that can be re-used to build own macros or have shortcuts assigned

origin - http://www.pipiscrew.com/?p=3263 sql-server-2008-addons