---
title: Backup the product activation of Microsoft Office
author: PipisCrew
date: 2017-02-27
categories: [app]
toc: true
---

Is able to backup the product activation of Microsoft Office XP, 2003, 2007, 2010 and 2013. After reinstalling Windows, it restores the backup so that there is no need for activating Office again (the hardware must be the same).

http://www.opa-backup.de/index_en.php

```js
// Microsoft Office XP
_versions[0] = new Version(10, "Microsoft Office XP", "OfficeXP", null);
_versions[0].AddRequiredFile(Path.Combine(licensePath, "data.dat"));
_versions[0].AddOptionalFile(Path.Combine(licensePath, "data.bak"));

// Microsoft Office 2003
_versions[1] = new Version(11, "Microsoft Office 2003", "Office2003", null);
_versions[1].AddRequiredFile(Path.Combine(licensePath, "opa11.dat"));
_versions[1].AddOptionalFile(Path.Combine(licensePath, "opa11.bak"));

// Microsoft Office 2007
_versions[2] = new Version(12, "Microsoft Office 2007", "Office2007", null);
_versions[2].AddRequiredFile(Path.Combine(licensePath, "opa12.dat"));
_versions[2].AddOptionalFile(Path.Combine(licensePath, "opa12.bak"));
_versions[2].AddOptionalDirectory(licensePath, "*.bpc");

// Microsoft Office 2010
_versions[3] = new Version(14, "Microsoft Office 2010", "Office2010", servicesToKill);
_versions[3].AddRequiredFile(Path.Combine(licensePath2010, "tokens.dat"));
_versions[3].AddOptionalFile(Path.Combine(licensePath2010, "data.dat"));
_versions[3].AddRequiredFile(Path.Combine(licensePath2010, "Cache\\cache.dat"));
```

origin - http://www.pipiscrew.com/?p=6909 backup-the-product-activation-of-microsoft-office