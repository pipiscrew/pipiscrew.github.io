---
title: Extracting a URL from a hyperlink on Excel
author: PipisCrew
date: 2019-09-17
categories: [vba]
toc: true
---

```js
'src - https://howtouseexcel.net/how-to-extract-a-url-from-a-hyperlink-on-excel
Sub Button1_Click()
    Dim HL As Hyperlink

    For Each HL In ActiveSheet.Hyperlinks
        HL.Range.Offset(0, 1).Value = HL.Address
    Next
End Sub
```

origin - https://www.pipiscrew.com/?p=15326 extracting-a-url-from-a-hyperlink-on-excel