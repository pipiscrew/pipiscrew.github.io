---
title: Merge cells with the same cell ID value!
author: PipisCrew
date: 2018-04-18
categories: [vba]
toc: true
---

reference
[http://www.excel-easy.com/vba/create-a-macro.html](http://www.excel-easy.com/vba/create-a-macro.html)
[http://www.excel-easy.com/vba/examples/loop-through-entire-column.html](http://www.excel-easy.com/vba/examples/loop-through-entire-column.html)
[http://www.excel-easy.com/vba/examples/write-data-to-text-file.html](http://www.excel-easy.com/vba/examples/write-data-to-text-file.html)

```js
Private Sub Button1_Click()
	Dim x As Integer
	Dim tmp As String

	//for all rows
	For i = 2 To Rows.Count
		tmp = ""

		If Len(Cells(i, 1).Value) > 0 Then
			If Cells(i, 1).Value = Cells(i - 1, 1).Value Then

				If (Len(Cells(i - 1, 3).Value) > 0) Then
					tmp = ""
				Else
					tmp = Cells(i - 1, 2).Value
				End If

				Cells(i, 3).Value = tmp & "," & Cells(i, 2).Value

			End If
		Else
			Exit Sub
		End If

	Next i

End Sub

'write to Sheet2
'Sheets("Sheet2").Range("A" & i) = Cells(i, 3).Value
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/02/snap410.png "snap410")

snippet : loop through sheet1 rows, match sheet1.code column with sheet2.code column, transfer (aka merge) sheet2 columns to sheet1
```js
Sub Button1_Click()
    Dim x As Integer
    Dim tmp As String

    Dim j
    For i = 2 To 771 'Rows.Count

        j = find_in_second(Cells(i, 2).Value)

        'MsgBox j(1, 1)

        If IsNull(j) = False Then
            For r = 1 To 67
                Cells(i, 19 + r).Value = j(1, r)
            Next
        End If

       ' Debug.Print i

    Next i

End Sub

Private Function find_in_second(code As String)
 For i = 2 To 913 'Sheets("Sheet2").Rows.Count

    If (Sheets("Sheet2").Cells(i, 8).Value = code) Then
        'return complete row
        find_in_second = Sheets("Sheet2").Rows(i).Value
        Exit For
    Else
        find_in_second = Null
    End If

 Next
End Function
```

Get the column of a user selected cell using vba excel
```js
'http://stackoverflow.com/a/22260714

Dim sheet1_search As Integer
Dim sheet2_find_to As Integer

sheet1_search = getcolumn("Please select the column contains the text referenced to source sheet", "Test")
sheet2_find_to = getcolumn("Please select the source column", "Test")

If (sheet1_search = 0 Or sheet2_find_to = 0) Then
	MsgBox ("Please select a valid column")
	Exit Sub
End If

Private Function getcolumn(prompt_text As String, title As String)
    Dim rng As Range
    On Error Resume Next
    Set rng = Application.InputBox(Prompt:=prompt_text, title:=title, Type:=8)
    On Error GoTo 0

    If rng Is Nothing Then
        getcolumn = 0
    Else
        getcolumn = rng.Column
    End If

End Function
```

Convert Greek Vowels on first column
```js
Sub Button1_Click()
    Dim i As Integer
    Dim tmp As String

    For i = 1 To Rows.Count
        tmp = ""

        tmp = Cells(i, 1).Value

        If Len(tmp) > 0 Then
            tmp = Replace(tmp, "Ά", "Α")
            tmp = Replace(tmp, "ά", "α")
            tmp = Replace(tmp, "Έ", "Ε")
            tmp = Replace(tmp, "έ", "ε")
            tmp = Replace(tmp, "Ώ", "Ω")
            tmp = Replace(tmp, "ώ", "ω")
            tmp = Replace(tmp, "Ύ", "Υ")
            tmp = Replace(tmp, "ύ", "υ")
            tmp = Replace(tmp, "Ί", "Ι")
            tmp = Replace(tmp, "ί", "ι")
            tmp = Replace(tmp, "Ό", "Ο")
            tmp = Replace(tmp, "ό", "ο")
            tmp = Replace(tmp, "Ή", "η")
            tmp = Replace(tmp, "ή", "η")

            tmp = Replace(tmp, "ς", "Σ")

            Cells(i, 1).Value = UCase(tmp)
        End If

    Next i
End Sub

```

Read a URL and set URL result to cell!
```js
'source - http://tipsformarketers.com/scrape-webpage-data-using-excel-vba/
Sub Button1_Click()
    Dim x As Integer
    Dim tmp As String
    Dim oHTTP As Object
    Dim url1 As String
    Dim url2 As String

    url1 = "https://www.google.com?q="
    url2 = "&ie=UTF-8"

    Set oHTTP = CreateObject("msxml2.ServerXMLHTTP")
    For i = 2 To Rows.Count
        tmp = ""

        If Len(Cells(i, 2).Value) > 0 Then
            oHTTP.Open "GET", url1 + Cells(i, 2).Value + url2, False
            oHTTP.send
            page_html = (oHTTP.responseText)

            If (Len(page_html) > 0) Then
                Cells(i, 3).Value = page_html
            End If

        Else
            Exit Sub
        End If

    Next i
End Sub

```

Cell Keypress
```js
'http://pdaphal.blogspot.com
Private Sub Worksheet_Change(ByVal Target As Range)
	If Target.Address = "$E$3" Then
		Call Macro1
	End If
End Sub
```

origin - http://www.pipiscrew.com/?p=2344 vba-merge-cells-with-the-same-cell-id-value