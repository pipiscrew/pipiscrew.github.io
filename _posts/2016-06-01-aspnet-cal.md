---
title: o[asp.net] call a c# button event by js
author: PipisCrew
date: 2016-06-01
categories: [js,asp.net]
toc: true
---

```js
//test_sync.aspx
<%@ Page Language="C#" %>

    protected void Page_Load(object sender, EventArgs e)
    {
        if (IsPostBack)
        {
            this.myDIV.InnerText = "is postback";
        }
        else
        {
            this.myDIV.InnerText = "first land";
        }
    }

    protected void savebtn_Click(object sender, EventArgs e)
    {
        System.Diagnostics.Debug.WriteLine("this is a test");
    }

        $(function () {

            //button click
            $('#btn').on('click', function (e) {
                e.preventDefault();

                $("#savebtn").click();

                $("#myDIV").html("ERROR");

                return false;
            });

        });

    <button id="btn" class="btn-primary">
        Push Me
    </button>

    <div id="myDIV" runat="server"></div>

    <form id="Form1" runat="server">

    <asp:button id="savebtn" runat="server" text="my aspx button" onclick="savebtn_Click" style="display: none"></asp:button>

    </form>

```

Using AsyncPostBackTrigger

```js
//test_async.aspx
<%@ Page Language="C#" %>

    protected void savebtn_Click(object sender, EventArgs e)
    {
        myDIV.InnerText = "this is a test";
        System.Diagnostics.Debug.WriteLine("this is a test");
    }

        $(function () {

            //button click
            $('#btn').on('click', function (e) {
                e.preventDefault();

                $("#savebtn").click();

                $("#myDIV").html("ERROR");
            });

        });

    <button id="btn" class="btn-primary">
        Push Me
    </button>

<form id="form1" runat="server">
 <asp:scriptmanager enablepartialrendering="true" runat="server"></asp:scriptmanager>

    <asp:updatepanel updatemode="Conditional" runat="server">
        <triggers>
            <asp:asyncpostbacktrigger controlid="savebtn"></asp:asyncpostbacktrigger>
        </triggers>
        <contenttemplate>

        <div id="myDIV" runat="server"></div>

         <asp:button id="savebtn" runat="server" text="my aspx button" onclick="savebtn_Click" style="display: none"></asp:button>
        </contenttemplate>
    </asp:updatepanel>

</form>

```

## or can use __doPostBack

[http://www.codeproject.com/Articles/667531/doPostBack-function](http://www.codeproject.com/Articles/667531/doPostBack-function)
[http://aspalliance.com/895_Understanding_the_JavaScript___doPostBack_Function.2](http://aspalliance.com/895_Understanding_the_JavaScript___doPostBack_Function.2)
[http://stackoverflow.com/a/3914500](http://stackoverflow.com/a/3914500)

## ScriptManager.RegisterStartupScript

ref - [https://msdn.microsoft.com/en-us/library/z9h4dk8y(v=vs.100).aspx](https://msdn.microsoft.com/en-us/library/z9h4dk8y(v=vs.100).aspx)

```js
<asp:updatepanel id="upMyTest" updatemode="Conditional" runat="server">
	<triggers>
		<asp:asyncpostbacktrigger controlid="btnRefreshTest"></asp:asyncpostbacktrigger>
	</triggers>
	<contenttemplate>

		<button id="btn">
			Push Me
		</button>

		<asp:button id="btnRefreshTest" clientidmode="Static" onclick="btnRefreshTest_Click" style="display: none" runat="server"></asp:button>

	</contenttemplate>
</asp:updatepanel>
```

```js
//code behind
protected void btnRefreshTest_Click(object sender, EventArgs e)
{
	BindTestData(); // #your# Test function

	//Javascript script - executed when the page finishes loading but before the page's OnLoad event is raised
	ScriptManager.RegisterStartupScript(this.btnRefreshTest, this.btnRefreshTest.GetType(), "refreshTestScript", "refreshTestOption();", true);
}
```

```js
//button click
$('#btn').on('click', function(e) {
	//invoke the update method
	$('#btnRefreshTest').click();
});

function refreshTestOption() {
	//#your# code here
}
```

### sample2

```js
<asp:updatepanel id="updPANEL" updatemode="Conditional" runat="server">
	<triggers>
		<asp:asyncpostbacktrigger controlid="btnCheckPlayer"></asp:asyncpostbacktrigger>
		<asp:asyncpostbacktrigger controlid="btnDeletePlayer"></asp:asyncpostbacktrigger>
	</triggers>
	<contenttemplate>
		<asp:button id="btnCheckPlayer" onclick="btnCheckPlayer_Click" cssclass="btn btn-check" style="height:31px;" text="Check" runat="server"></asp:button>
		<asp:button id="btnDeletePlayer" onclick="btnDeletePlayer_Click" cssclass="btn btn-danger" style="height:31px;" text="Delete" runat="server" visible="false"></asp:button>
		<div id="divPlayerError" clientidmode="static" style="display:none; width: 100%;padding: 10px;background-color:#F5F5F5;margin: 10px 0 10px 0;" runat="server"></div>
	</contenttemplate>
</asp:updatepanel>

protected void btnCheckPlayer_Click(object sender, EventArgs e)
{
	Session["Player_used"] = 1;
	Session["Player_code_used"] = this.txtPlayerCode.Text;

	this.divPlayerError.InnerHtml = "Player Checked";

	this.updPANEL.Update();
	ScriptManager.RegisterStartupScript(this.Page, this.Page.GetType(), "ePlayerError", "$(function(){ $('#divPlayerError').show(); setTimeout(function(){ $('#divPlayerError').hide(); }, 5000); });", true);
}

protected void btnDeletePlayer_Click(object sender, EventArgs e)
{
	if (Session["Player_used"] != null && Session["Player_code_used"] != null)
	{
		int k;

		if (int.TryParse(Session["Player_used"].ToString(), out k))
		{
			Session["Player_used"] = Session["Player_code_used"] = null;

			this.divPlayerError.InnerHtml = "Player Deleted";

			btnDeletePlayer.Visible = false;
			btnCheckPlayer.Visible = true;

			this.updPANEL.Update();
			ScriptManager.RegisterStartupScript(this.Page, this.Page.GetType(), "ePlayerError", "$(function(){ $('#divPlayerError').show(); setTimeout(function(){ $('#divPlayerError').hide(); }, 5000); });", true);
		}
		else
		{
			this.divPlayerError.InnerHtml = "Player not found";
			ScriptManager.RegisterStartupScript(this.Page, this.Page.GetType(), "ePlayerError", "$(function(){ $('#divPlayerError').show(); setTimeout(function(){ $('#divPlayerError').hide(); }, 5000); });", true);
		}

	}
}
```

origin - http://www.pipiscrew.com/?p=2270 asp-net-call-a-c-button-event-by-js