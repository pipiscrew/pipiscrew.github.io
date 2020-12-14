---
title: Compare all cells of two Excel files or sheets
author: PipisCrew
date: 2018-04-18
categories: [vba,vba]
toc: true
---

@Jean-François Corbett - Load an entire sheet at once into a Variant array. In Excel 2003, this takes about 2 seconds (and 250 MB of RAM). Then you can loop through it in no time at all.

```js
'src - https://stackoverflow.com/a/5388488/1320686
Option Explicit

Sub test()

    Dim varSheetA As Variant
    Dim varSheetB As Variant
    Dim strRangeToCheck As String
    Dim iRow As Long
    Dim iCol As Long

    strRangeToCheck = "A1:IV65536"
    ' If you know the data will only be in a smaller range, reduce the size of the ranges above.
    Debug.Print Now
    varSheetA = Worksheets("Sheet1").Range(strRangeToCheck)
    varSheetB = Worksheets("Sheet2").Range(strRangeToCheck) ' or whatever your other sheet is.
    Debug.Print Now

    For iRow = LBound(varSheetA, 1) To UBound(varSheetA, 1)
        For iCol = LBound(varSheetA, 2) To UBound(varSheetA, 2)
            If varSheetA(iRow, iCol) = varSheetB(iRow, iCol) Then
                ' Cells are identical.
                ' Do nothing.
            Else
                ' MsgBox (iRow & "," & iCol)
                ' Debug.Print (iRow & "," & iCol)
                ' Cells are different.
                ' Code goes here for whatever it is you want to do.
            End If
        Next iCol
    Next iRow

End Sub

'To compare to a sheet in a different workbook, open that workbook and get the sheet as follows:

'Set wbkA = Workbooks.Open(filename:="C:\MyBook.xls")
'Set varSheetA = wbkA.Worksheets("Sheet1") ' or whatever sheet you need 
```

#vba #compare

origin - http://www.pipiscrew.com/?p=13377 compare-all-cells-of-two-excel-files-or-sheets