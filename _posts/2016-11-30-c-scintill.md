---
title: o[c#] ScintillaNET
author: PipisCrew
date: 2016-11-30
categories: [.net]
toc: true
---

ScintillaNET - https://github.com/jacobslusser/ScintillaNET
ScintillaNET - FindReplaceDialog - https://github.com/Stumpii/ScintillaNET-FindReplaceDialog
ScintillaNET Syntaxthighlight Designer - https://github.com/uuf6429/ScintillaNET-Kitchen
Automatic Syntax Highlighting - https://github.com/jacobslusser/ScintillaNET/wiki/Automatic-Syntax-Highlighting

```js
--src - SQL Syntaxthighlight - https://github.com/jacobslusser/ScintillaNET/issues/134
scintilla1.CaretForeColor = Color.White;

scintilla1.Margins[0].Width = 16;

scintilla1.StyleResetDefault();
scintilla1.Styles[Style.Default].Font = "Consolas";
scintilla1.Styles[Style.Default].Size = 10;
scintilla1.Styles[Style.Default].BackColor = Color.FromArgb(41, 49, 52);
scintilla1.StyleClearAll();

scintilla1.Lexer = Lexer.Sql;

scintilla1.Styles[Style.Sql.Word].ForeColor = Color.FromArgb(147, 199, 99);
scintilla1.Styles[Style.Sql.Word].Bold = true;
scintilla1.Styles[Style.Sql.Identifier].ForeColor = Color.FromArgb(255, 255, 255);
scintilla1.Styles[Style.Sql.Character].ForeColor = Color.FromArgb(236, 118, 0);
scintilla1.Styles[Style.Sql.Number].ForeColor = Color.FromArgb(255, 205, 34);
scintilla1.Styles[Style.Sql.Operator].ForeColor = Color.FromArgb(232, 226, 183);
scintilla1.Styles[Style.Sql.Comment].ForeColor = Color.FromArgb(102, 116, 123);
scintilla1.Styles[Style.Sql.CommentLine].ForeColor = Color.FromArgb(102, 116, 123);

scintilla1.SetKeywords(0, "add alter as asc authorization backup begin break browse bulk by cascade case check checkpoint close clustered column commit compute constraint containstable continue create current current_date cursor database dbcc deallocate declare default delete deny desc disk distinct distributed double drop dump else end errlvl escape except exec execute exit external fetch file fillfactor for foreign freetext freetexttable from full function goto grant group having holdlock identity identity_insert identitycol if index insert intersect into key kill lineno load merge national nocheck nonclustered of off offsets on open opendatasource openquery openrowset openxml option order over percent plan precision primary print proc procedure public raiserror read readtext reconfigure references replication restore restrict return revert revoke rollback rowcount rowguidcol rule save schema securityaudit select semantickeyphrasetable semanticsimilaritydetailstable semanticsimilaritytable set setuser shutdown statistics table tablesample textsize then to top tran transaction trigger truncate union unique updatetext use user values varying view waitfor when where while with within group writetext coalesce collate contains convert current_time current_timestamp current_user nullif session_user system_user try_convert tsequal update all and any between cross exists in inner is join left like not null or outer pivot right some unpivot");
```

```js
//can replace this 
private void txtSQL_KeyUp(object sender, KeyEventArgs e)
{
	if (e.KeyCode == Keys.F5)
	{
		if (txtSQL.SelectedText.Length > 0)
			runSQL(txtSQL.SelectedText);
		else
			runSQL(txtSQL.Text);

		//((TextBox)sender).SelectAll();
		e.Handled = true;
	}
}
```

#syntax #highlighting

origin - http://www.pipiscrew.com/?p=6333 c-scintillanet