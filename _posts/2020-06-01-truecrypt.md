---
title: TrueCrypt
author: PipisCrew
date: 2020-06-01
categories: [app]
toc: true
---

WARNING: Using TrueCrypt is not secure as it may contain unfixed security issues. 

homepage 
[http://truecrypt.sourceforge.net/](http://truecrypt.sourceforge.net/)

makeuseof
[http://www.makeuseof.com/tag/encrypted-folders-truecrypt-7/](http://www.makeuseof.com/tag/encrypted-folders-truecrypt-7/)

## boxcryptor (java based)

https://www.boxcryptor.com/
https://www.boxcryptor.com/en/boxcryptor-portable-download

## AxCrypt with Source Code 

http://www.axantum.com/
http://www.axantum.com/AxCrypt/SourceCode.aspx

## DiskCryptor with Source Code 

https://sourceforge.net/projects/diskcryptor/

## Softwares based on TrueCrypt source code :

[https://veracrypt.codeplex.com](https://veracrypt.codeplex.com)
[https://ciphershed.org/](https://ciphershed.org/)
VeraCrypt is compatible the TrueCrypt containers.

Original authors maintain the project to [https://truecrypt.ch/](https://truecrypt.ch/)
mtcrypt - TrueCrypt GUI (mount/unmount easily) - [https://code.google.com/p/mtcrypt/](https://code.google.com/p/mtcrypt/)

comparison matrix - https://www.comparitech.com/blog/information-security/disk-encryption-software/

## howto create hidden container

[http://www.howtogeek.com/109210/the-htg-guide-to-hiding-your-data-in-a-truecrypt-hidden-volume/](http://www.howtogeek.com/109210/the-htg-guide-to-hiding-your-data-in-a-truecrypt-hidden-volume/)

https://www.youtube.com/watch?v=eUCBodVS3AE

## truecrypt commandline

[http://andryou.com/truecrypt/docs/command-line-usage.php](http://andryou.com/truecrypt/docs/command-line-usage.php)
[http://fourwestmedia.com/resources/how-to-guides/truecrypt-using-batch-scripts-to-mount-and-dismount-volumes/#tcbat2](http://fourwestmedia.com/resources/how-to-guides/truecrypt-using-batch-scripts-to-mount-and-dismount-volumes/#tcbat2)

```js
//A simple batch script to mount a USB drive as a removable disk:
//Volume mounted to 'x' in this case
TrueCrypt /v myvolume.tc /lx /m rm /a /e /q

//A simple batch script to dismount an encrypted volume:
//Volume currently mounted on 'x' in this case
TrueCrypt /q /dx

//A simple batch script to dismount all encrypted volumes:
TrueCrypt /q /d
```

> TrueCrypt automatically dismounts its volumes when Windows is shutting down. Even on portable mode
> (i.e. the user is "logged off" and there is a setting for auto-dismount when this happens.)

source - [http://superuser.com/a/891030](http://superuser.com/a/891030)

> Even when the power supply is suddenly interrupted (without proper system shutdown), all files stored on the volume will be inaccessible (and encrypted).

source - [http://www.utexas.edu/its/secure/articles/truecrypt-pc.php](http://www.utexas.edu/its/secure/articles/truecrypt-pc.php)

## FreeOTFE

[http://sourceforge.net/projects/freeotfe.mirror/](http://sourceforge.net/projects/freeotfe.mirror/)

--fake protection--
//csharp ghost like project
[http://www.codeproject.com/Articles/20880/Folder-protection-for-Windows-using-Csharp-and-con](http://www.codeproject.com/Articles/20880/Folder-protection-for-Windows-using-Csharp-and-con)

origin - http://www.pipiscrew.com/?p=1802 app-truecrypt