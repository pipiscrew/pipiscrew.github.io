---
title: Convert Salesforce record ID 15 digit to 18 digit conversion
author: PipisCrew
date: 2018-02-12
categories: [news]
toc: true
---

Every record in salesforce is identified by unique record ID in every salesforce organization.
-15 digit case-sensitive version is referenced in the UI and also visible in browser (case sensitive)
-18 digit case-insensitive version which is referenced through the API (case insensitive, the last 3 digits of the 18 digit ID is a checksum of the capitalization of the first 15 characters,  API will accept the 15 digit Id as input but will always return the 18 digit ID)

in apex flavor 
http://www.sfdcpoint.com/salesforce/salesforce-id-15-digit-18-digit-conversion/

in JS flavor 
https://www.adminbooster.com/tool/15to18

origin - https://www.pipiscrew.com/2018/02/convert-salesforce-record-id-15-digit-to-18-digit-conversion/ convert-salesforce-record-id-15-digit-to-18-digit-conversion