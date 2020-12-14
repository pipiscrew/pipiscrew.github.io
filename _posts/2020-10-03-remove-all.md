---
title: Remove All Pictures From Document In Word
author: PipisCrew
date: 2020-10-03
categories: [news]
toc: true
---

### 1 way )

Go to Developer tab, Visual Basic, paste

```js
Public Sub PicturesDeleteAll()

Dim objPic As Shape

    For Each objPic In ActiveDocument.Shapes
            objPic.Delete
    Next objPic

Dim objPic2 As InlineShape
    For Each objPic2 In ActiveDocument.InlineShapes
            objPic2.Delete
    Next objPic2
End Sub

```

on my tests, multiple **run** needed

then **remove** the macro.

ref
https://superuser.com/a/675136

### 2 way )

In the **Find and Replace** window, click the **More>>** button to bring up more Search Options, and then click **Special** > Graphic, and finally click the Replace All button. [src](https://www.extendoffice.com/documents/word/717-word-remove-picture.html)

origin - https://www.pipiscrew.com/?p=19162 remove-all-pictures-from-document-in-word