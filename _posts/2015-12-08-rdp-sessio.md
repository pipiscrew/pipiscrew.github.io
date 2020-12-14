---
title: RDP sessions with PowerShell
author: PipisCrew
date: 2015-12-08
categories: [news]
toc: true
---

Windows PowerShell ISE editor - [http://www.powertheshell.com/](http://www.powertheshell.com/)

### the script itself from commandline : 

[http://irisclasson.com/2015/12/03/saving-rdp-sessions-with-posh/](http://irisclasson.com/2015/12/03/saving-rdp-sessions-with-posh/)

### make script, scriptfile :

-at windows explorer create a new file yourname.ps1
-edit yourname.ps1
```js
$target = "ThePC" #use computer name or IP

$pdw = "12345"

$logon = "administrator"

cmdkey /generic:$target /user:$logon #/pass:$pwd

cmdkey /list

mstsc /v:$target
```

now, when left-click 
![Snap437](https://www.pipiscrew.com/wp-content/uploads/2015/12/Snap437.png)

### execute the script by PowerShell

![snap448](https://www.pipiscrew.com/wp-content/uploads/2015/12/snap448.png)

You can run a script via :
![snap449](https://www.pipiscrew.com/wp-content/uploads/2015/12/snap449.png)
```js
<!--
http://windowsitpro.com/powershell/running-powershell-scripts-easy-1-2-3
http://ss64.com/ps/syntax-run.html
 -->

Set-ExecutionPolicy RemoteSigned

script.ps1
```

The Modules Directory, By Default exists at : 
```js
C:\Windows\System32\WindowsPowerShell\v1.0\Modules
```

* * *

### Why PowerShell?

[https://ramblingcookiemonster.wordpress.com/2013/12/07/why-powershell/](https://ramblingcookiemonster.wordpress.com/2013/12/07/why-powershell/)

### PowerShell Resources

[http://ramblingcookiemonster.github.io/Pages/PowerShellResources.html](http://ramblingcookiemonster.github.io/Pages/PowerShellResources.html)

### PowerShellJS

[https://github.com/klumsy/PowerShellJS](https://github.com/klumsy/PowerShellJS)

### Set of commands to install PowerShell modules from local file or from the web.

[http://psget.net/](http://psget.net/)
[https://github.com/psget/psget/](https://github.com/psget/psget/)

origin - http://www.pipiscrew.com/?p=2732 rdp-sessions-with-powershell