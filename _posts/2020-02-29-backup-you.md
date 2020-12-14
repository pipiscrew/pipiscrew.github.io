---
title: Backup your Gmail and Gapps data
author: PipisCrew
date: 2020-02-29
categories: [news]
toc: true
---

https://gmail.googleblog.com/2013/12/download-copy-of-your-gmail-and-google.html

open/browse mbox file with freeware
https://www.bitrecover.com/free/mbox-viewer/ (super extra speed)
https://sourceforge.net/projects/mbox-viewer/

use thunderbird addon to import it (attachments supported) ([ref](https://lifehacker.com/how-to-back-up-your-gmail-and-view-mbox-files-1827660389))
[Paolo.ImportExportTools](https://addons.thunderbird.net/en-US/thunderbird/addon/importexporttools/)  supports Thunderbird v14.0 - v60.x

2020 update

tested&working Thunderbird v68.5 with [ImportExportTools NG](https://addons.thunderbird.net/en-US/thunderbird/addon/importexporttools-ng) (attachments supported) supports Thunderbird v60.0 - v69.x

--

If you still want to use Outlook (convert mbox to pst), use the paid [MBOX Converter Wizard](https://www.bitrecover.com/mbox-converter/).

If you want to do it manual (export all emails to separate .eml files, attachments supported), use [got-your-back](https://github.com/jay0lee/got-your-back/) by jay0lee. Supports restoration by the eml or mbox.

by my tests, the best option is with Thunderbird (no credentials, export from gmail a file, import it), jay0lee solution is long standing.

--

## Restore emails online

Mozilla Thunderbird, is able to open .mbox files with an addon. After you'll need to add the G Suite/Gmail account as IMAP and start Copy/Paste messages from the archived folder to the active account. [src](https://productforums.google.com/forum/#!topic/apps/5YCL_a1YMnI)

Simply import the MBOX file to a folder contained in your Gmail account and your data will be effectively moved/migrated! [src](https://spinbackup.com/blog/how-to-import-mbox-to-gmail/)

origin - http://www.pipiscrew.com/?p=10576 download-a-copy-of-your-gmail-and-gapps-data