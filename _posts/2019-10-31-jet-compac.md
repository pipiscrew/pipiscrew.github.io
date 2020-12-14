---
title: Jet compact utility
author: PipisCrew
date: 2019-10-31
categories: [app]
toc: true
---

> 3197	The Microsoft Jet database engine stopped the process because you and another user are attempting to change the same data at the same time.
> 3343	Unrecognized database format ‘databasename.mdb'.
> 3015	‘databasename.mdb' isn't an index in this table.  Look in the Indexes collection of the TableDef object to determine the valid index names.

The Jet compact utility, jetcomp.exe, is a stand-alone utility that compacts databases created with Microsoft Jet database engine 3.x and 4.x. This utility may be run in conjunction with Microsoft Jet database engine 3.x and 4.x for recovering corrupted databases.

Although you can run the Microsoft Access Compact utility or the CompactDatabase method with Microsoft Jet database engine 3.x and 4.x, Jetcomp.exe may be able to recover some databases that these utilities cannot. The reason for this is that the Microsoft Access Compact utility and the CompactDatabase method attempt to open and close a database before attempting to compact it. In certain cases where these utilities may not be able to reopen the database, Compact will be unable to proceed, preventing recovery of the database. jetcomp.exe does not attempt to open and close the database before compacting, and may therefore be able to recover some databases that the Microsoft Access compact utility and the CompactDatabase method cannot. [src](http://www.accessdatabaserepair.com/jetcomp.htm)

    1.Double-click JetComp.exe.
    2.In the Database to Compact From (Source) box, type the path and name of the database that you want to compact.
    3.In the Database to Compact Into (Destination) box, type the path and name of the new compacted database that you want to create.
    4.Under Additional Compact Options, set the appropriate options.
    5.Click Compact.

[download from microsoft](https://support.microsoft.com/en-in/help/295334/jet-compact-utility-is-available-in-download-center)

ref article - https://social.technet.microsoft.com/wiki/contents/articles/53151.microsoft-access-jetcomp-exe.aspx

ref - https://www.access-programmers.co.uk/forums/showthread.php?t=36029

#jetcomp.exe #JetCompactUtility

origin - https://www.pipiscrew.com/?p=15620 jet-compact-utility