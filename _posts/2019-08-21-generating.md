---
title: Generating AES256 Keys with PowerShell
author: PipisCrew
date: 2019-08-21
categories: [news]
toc: true
---

```js
//src - http://lennybacon.com/post/Generating-AES256-Keys-with-PowerShell

$random = [System.Security.Cryptography.RandomNumberGenerator]::Create();
$buffer = New-Object byte[] 32;
$random.GetBytes($buffer);
[BitConverter]::ToString($buffer).Replace("-", [string]::Empty);
```

#powershell

origin - https://www.pipiscrew.com/?p=15255 generating-aes256-keys-with-powershell