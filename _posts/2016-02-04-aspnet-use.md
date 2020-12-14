---
title: o[asp.net] usercontrol - ascx
author: PipisCrew
date: 2016-02-04
categories: [asp.net]
toc: true
---

### Compile ASP.NET WebForms .ascx UserControls into Assembly for Re-Use

[https://kocubinski.wordpress.com/2013/05/06/compile-asp-net-webforms-ascx-usercontrols-into-assembly-for-re-use/](https://kocubinski.wordpress.com/2013/05/06/compile-asp-net-webforms-ascx-usercontrols-into-assembly-for-re-use/)

### Compile web application project ascx into dll

[http://stackoverflow.com/a/6899945](http://stackoverflow.com/a/6899945)

FYI **ascx** everytime 'loaded' compiled..

* * *

### Compiling ASCX files into a class library

[http://rossipedia.com/blog/2012/07/compiling-ascx-files-into-a-class-library/](http://rossipedia.com/blog/2012/07/compiling-ascx-files-into-a-class-library/)

CodeFile vs CodeBehind - [http://stackoverflow.com/a/954873](http://stackoverflow.com/a/954873)

You’ll need to make sure you download and install ILMerge in order for this to work. These steps assume the default install location.

Start with an empty C# class library project, and add a reference to System.Web.

Add your control. For this example I’m just going to use the following super basic control (named MyControl.ascx):
```js
//MyControl.ascx
<%@ Control Language="C#" ClassName="ControlTest.MyControl"
CodeFile="MyControl.ascx.cs" Inherits="ControlTest.MyControlCode"
AutoEventWireup="true" %>

<asp:multiview runat="server" id="mvName">
<views>
   <asp:view runat="server" id="vwDisplay">
       Your name is <asp:label runat="server" id="lblName"></asp:label>
       <asp:button runat="server" id="btnReset" onclick="ResetButtonClick" text="Reset Name"></asp:button>
   </asp:view>
   <asp:view runat="server" id="vwInput">
       Enter your name: <asp:textbox runat="server" id="txtName"></asp:textbox>
       <asp:button runat="server" id="btnSet" onclick="SetButtonClick" text="Set Name"></asp:button>
   </asp:view>
</views>
</asp:multiview>
```

Note: You’ll have to add this by selecting “Text File” as Class Library projects don’t give you the web control templates.

A couple of important things to note:

The CodeFile attribute is used instead of the CodeBehind attribute. This is due to  the fact that the ASP.NET compiler ignores files referenced by CodeBehind.
The ClassName attribute is used so that we can specify what class name we want (including the namespace). Otherwise, we’d have to resort to using silly things like . And that’s just silly.
Here’s the contents of my MyControl.ascx.cs file:
```js
//MyControl.ascx.cs
namespace ControlTest
{
    using System;
    using System.Web.UI;

    public partial class MyControlCode : UserControl
    {
        public void Page_Load(object sender, EventArgs e)
        {
                if(!IsPostBack)
                {
                        this.mvName.SetActiveView(this.vwInput);
                }
        }

        public void SetButtonClick(object sender, EventArgs e)
        {
                this.lblName.Text = this.txtName.Text;
                this.mvName.SetActiveView(this.vwDisplay);
        }

        public void ResetButtonClick(object sender, EventArgs e)
        {
                this.lblName.Text = string.Empty;
                this.mvName.SetActiveView(this.vwInput);
        }
    }
}
```

* * *

## Load dynamic .ascx

method into page w/ parent System.Web.UI.Page
```js
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        GetDynamicPageCodeFromFile();
    }

    public void GetDynamicPageCodeFromFile()
    {
        UserControl viewControl = null;
        try
        {
            viewControl = (UserControl)this.LoadControl("~/WebUserControl1.ascx");
        }
        catch (Exception)        {        }

        if (viewControl != null) this.Controls.Add(viewControl);
    }
}
```

method in diff class (using inheritance)
```js
//General.cs
public class General : System.Web.UI.Page
{
	public void GetDynamicPageCodeFromFile()
	{
		UserControl viewControl = null;
		try
		{
			viewControl = (UserControl)this.LoadControl("~/WebUserControl1.ascx");
		}
		catch (Exception)        {        }

		if (viewControl != null) this.Controls.Add(viewControl);
	}
}

//Default2.aspx.cs
public partial class Default2 : General
{
    protected void Page_Load(object sender, EventArgs e)
    {
        GetDynamicPageCodeFromFile();
    }
}

//Default2.aspx (remains as is)
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default2.aspx.cs" Inherits="Default2" %>
```

* * *

## Use .ascx on .aspx

```js
//WebUserControl1.ascx
<%@ Control Language="C#" AutoEventWireup="true" CodeBehind="WebUserControl1.ascx.cs" Inherits="WebApplication6ascx.WebUserControl1" %>

**------------------------------------------**
~~TEST~~
**------------------------------------------**

//WebForm1.aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="WebApplication6ascx.WebForm1" %>

<%@ Register TagPrefix="uc" TagName="Spinner" 
    Src="~/WebUserControl1.ascx" %>

    <form id="Form1" runat="server">
        <uc:spinner id="Spinner1" runat="server"></uc:spinner>
    </form>

```

origin - http://www.pipiscrew.com/?p=3465 asp-net-usercontrol-ascx