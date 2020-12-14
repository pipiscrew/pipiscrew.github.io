---
title: vlookup in vba
author: PipisCrew
date: 2018-05-08
categories: [vba]
toc: true
---

```js

'src - https://www.exceltrick.com/formulas_macros/vlookup-in-vba/

Sub FINDSAL()
	On Error GoTo MyErrorHandler:
	Dim E_name As String
	E_name = InputBox("Enter the Employee Name :")
	If Len(E_name) > 0 Then
		Sal = Application.WorksheetFunction.VLookup(E_name, Sheet1.Range("B3:D13"), 3, False)
		MsgBox "Salary is : $ " & Sal
	Else
		MsgBox ("You entered an invalid value")
	End If
	Exit Sub
	MyErrorHandler:
	If Err.Number = 1004 Then
		MsgBox "Employee Not Present in the table."
	End If
End Sub

```

origin - http://www.pipiscrew.com/?p=13651 vlookup-in-vba