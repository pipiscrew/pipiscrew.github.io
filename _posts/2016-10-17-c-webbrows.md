---
title: o[c#] WebBrowser - Execute custom Javascript to a page
author: PipisCrew
date: 2016-10-17
categories: [.net]
toc: true
---

```js
private void frmTest_Load(object sender, EventArgs e)
{
	this.Enabled = false;
	webBrowser1.Navigate("http://thepage.com");
	webBrowser1.DocumentCompleted += webBrowser1_DocumentCompleted;
	timer1.Interval = 100;
}

private void webBrowser1_DocumentCompleted(object sender, WebBrowserDocumentCompletedEventArgs e)
{
    //http://stackoverflow.com/a/7801574
    //inject JS to current page, and execute it!!

    //check a checkbox - via jQuery (already loaded by the original page, otherwise use plain js)
    var jsCode = "$(\"#chk_goal\").prop('checked',true);";
    webBrowser1.Document.InvokeScript("execScript", new Object[] { jsCode, "JavaScript" });

    //checkbox is checked here

    //execute a mouse click to the page
    timer1.Enabled = true;
}

//make a click to an element - macro style
private void timer1_Tick(object sender, EventArgs e)
{
    timer1.Enabled = false;
    Cursor.Position = new System.Drawing.Point(webBrowser1.Location.X + this.Location.X + 550, webBrowser1.Location.Y + this.Location.Y + 270);

    //http://stackoverflow.com/a/2416762
    int X = Cursor.Position.X;
    int Y = Cursor.Position.Y;
    mouse_event(MOUSEEVENTF_LEFTDOWN | MOUSEEVENTF_LEFTUP, X, Y, 0, 0);

    this.Enabled = true;
}
```

origin - http://www.pipiscrew.com/?p=6193 c-webbrowser-execute-custom-javascript-to-a-page