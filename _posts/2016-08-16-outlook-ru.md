---
title: Outlook Rules - Take Extra Actions
author: PipisCrew
date: 2016-08-16
categories: [news]
toc: true
---

- The ability to call a script from a rule is available to Outlook 2002 and later. 
- Creating the Script, Click Tools > Macro > Visual Basic Editor, or press ALT+F11.

```js
    Sub MyRule(Item As Outlook.MailItem)
        'Your custom VBA code goes here'
    End Sub
```

- Click Tools > Rules and Alerts.
- Click the New Rule button. Click Next. Select the "run a script" action, or run application!.
- In the lower panel click "a script" and select the script you created in step 1.

source - https://www.experts-exchange.com/articles/420/Extending-Outlook-Rules-via-Scripting.html

origin - http://www.pipiscrew.com/?p=6016 outlook-rules-take-extra-actions