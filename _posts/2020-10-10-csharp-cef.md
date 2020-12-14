---
title: o[csharp] CefSharp hints
author: PipisCrew
date: 2020-10-10
categories: [js,.net]
toc: true
---

reference
[http://github.com/cefsharp/CefSharp/wiki/Trouble-Shooting](http://github.com/cefsharp/CefSharp/wiki/Trouble-Shooting)
[http://github.com/cefsharp/CefSharp/wiki/Frequently-asked-questions#CallJS](http://github.com/cefsharp/CefSharp/wiki/Frequently-asked-questions#CallJS)
[framework requirements per version](https://github.com/cefsharp/CefSharp#release-branches)

.NET (WPF and Windows Forms) bindings for the Chromium Embedded Framework

This project contains .NET CLR bindings for The Chromium Embedded Framework (CEF) by Marshall A. Greenblatt. A small Core of the bindings are written in C++/CLI but the majority of code here is C#. It can of course be used from any CLR language, e.g. C# or VB.

[http://github.com/cefsharp/CefSharp](http://github.com/cefsharp/CefSharp)

<span style="color: #ff0000;">**to use CEFv3 - VC++ 2012 runtimes required   [download](https://www.microsoft.com/en-us/download/details.aspx?id=30679)**</span>

> your first app

```js
        //the browser
        //when CefSharpv1 - private readonly WebView web_view;
        private readonly ChromiumWebBrowser web_view; //CefSharpv3

        public Form1()
        {
            InitializeComponent();

            //when CefSharpv1 - web_view = new WebView("http://x.com/", new BrowserSettings());

            //required when CefSharpv3
            Cef.Initialize(new CefSettings()); //(CefSharp.Core required)
            web_view = new ChromiumWebBrowser("http://x.com/api/"); //CefSharpv3

            web_view.Dock = DockStyle.Fill;
            this.Controls.Add(web_view);
        }
```

> how to read the cookies

```js
//more https://github.com/cefsharp/CefSharp/issues/826
.
.
//somewhere in form
            //when CefSharpv1 - CEF.VisitAllCookies(new webview_cookies());
            Cef.VisitAllCookies(new webview_cookies()); //CefSharpv3 (CefSharp.Core required)
.
.
    class webview_cookies : ICookieVisitor
    {
        public bool Visit(Cookie cookie, int count, int total, ref bool deleteCookie)
        {
            //here you can store the cookie value to a static class

            Console.WriteLine(cookie.Name +" = " +  cookie.Value);

            return true;
        }
    }
```

> how to disable browser context menu (aka disable view source)

```js

        public Form1()
        {
            InitializeComponent();
.
.//init browser 
.
            web_view.MenuHandler = new  webview_menu();
        }

    class webview_menu : IMenuHandler
    {
        public bool OnBeforeMenu(IWebBrowser browser)
        {
            return true;
        }
    }
```

> Redirect user to another URL by code

```js
        //where the browser named
        private readonly WebView web_view;

        //on a button
        web_view.Load("https://pipiscrew.com/");

        //or load html via :
        web_view.LoadHtml("**Please wait!**");

        //reload page and ignore cache
        web_view.Reload(true);
```

> sniffing url + autofill elements via Javascript on the fly

```js
        public Form1()
        {
            InitializeComponent();

            Cef.Initialize(new CefSettings());

            web_view = new ChromiumWebBrowser("http://x.com/");
            web_view.FrameLoadEnd += new EventHandler<frameloadendeventargs>(web_view_FrameLoadEnd); //when CefSharpv1 -- .LoadCompleted += new LoadCompletedEventHandler(web_view_LoadCompleted);
            web_view.Dock = DockStyle.Fill;

            panel1.Controls.Add(web_view);
        }

        void web_view_FrameLoadEnd(object sender, FrameLoadEndEventArgs e)
        {
            if (e.Url.ToLower().StartsWith("https://www.x.com/login.php?skip_api_login"))
            {
                web_view.ExecuteScriptAsync("document.getElementById('email').value=" + '\'' + General.login_name + '\'');
                web_view.ExecuteScriptAsync("document.getElementById('pass').value=" + '\'' + General.login_password + '\'');
                web_view.ExecuteScriptAsync("document.getElementById('login_form').submit();");
                //web_view.ExecuteScript("document.getElementsByName('login').click()");
            }
        }
```

> Browser Settings - change useragent / use cache / store cookies (CefSharp3 only)

```js
        //reference - https://github.com/cefsharp/CefSharp/blob/master/CefSharp.Example/CefExample.cs

        //the browser
        private readonly ChromiumWebBrowser web_view;
        private readonly string cache_dir = Application.StartupPath + "\\tmp";

        public Form1()
        {
            InitializeComponent();

            Directory.CreateDirectory(cache_dir);

////
            var settings = new CefSettings();
            settings.UserAgent = "pipiscrew_browser_v" + Cef.CefSharpVersion;

            //the location where cache data will be stored on disk. If empty an in-memory cache will be used
            //http://magpcss.org/ceforum/apidocs3/projects/%28default%29/_cef_settings_t.html#cache_path        
            settings.CachePath = Application.StartupPath;

            //enable store cookies - method1
            //To persist session cookies (cookies without an expiry date or validity interval)
            settings.CefCommandLineArgs.Add("persist_session_cookies", "1");

            Cef.Initialize(settings);

            //enable store cookies - method2
            //To persist session cookies (cookies without an expiry date or validity interval)
            //Cef.SetCookiePath(cache_dir, true);
////
            web_view = new ChromiumWebBrowser("http://x.com/");
            web_view.Dock = DockStyle.Fill;
        }
```

> How to download file ?

```js
.
.
web_view = new ChromiumWebBrowser("http://x.com/");
web_view.DownloadHandler = new DownloadHandler();
.
.
    //used to download file - https://github.com/cefsharp/CefSharp/blob/master/CefSharp.Example/DownloadHandler.cs
    public class DownloadHandler : IDownloadHandler
    {
        public bool OnBeforeDownload(DownloadItem downloadItem, out string downloadPath, out bool showDialog)
        {
            downloadPath = downloadItem.SuggestedFileName;
            showDialog = true;

            return true;
        }

        public bool OnDownloadUpdated(DownloadItem downloadItem)
        {
            return false;
        }
    }
```

> From JS call NET function

```js
// tested&working with v39 - src - https://stackoverflow.com/a/23425179/1320686
// for newer versions - https://github.com/cefsharp/CefSharp/wiki/Frequently-asked-questions#CallJS
web_view.RegisterJsObject("callbackObj", new CallbackObjectForJs());

.
.
.

public class CallbackObjectForJs
{
	public void showMessage(string msg)
	{
		MessageBox.Show(msg);
	}
}

.
.
.

void web_view_FrameLoadEnd(object sender, FrameLoadEndEventArgs e)
{
	Console.WriteLine(e.Url.ToLower());
	if (e.Url.ToLower().StartsWith("https://www.x.com/login.php?skip_api_login"))
	{
		//inject your javascript
		web_view.ExecuteScriptAsync(x.Properties.Resources.script);
	}
}

.
.
.

//x.Properties.Resources.script

    callbackObj.showMessage('message from js');

/////////////////////// 2020 - CefSharp v79.x ////////////////////

//src - https://github.com/cefsharp/CefSharp/issues/2990
CefSharpSettings.LegacyJavascriptBindingEnabled = true;
CefSharpSettings.WcfEnabled = true;
.
.
web_view.JavascriptObjectRepository.Register("callbackObj", new CallbackObjectForJs(), isAsync: false, options: BindingOptions.DefaultBinder);
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/02/snap5061.png "snap506")

![](https://www.pipiscrew.com/wp-content/uploads/2015/02/snap507.png "snap507")

* * *

as for **cefsharp.common.79.1.360**, downloading nuget packages, rename it to **.zip**, inside **CefSharp** folder is **precompiled** the **dlls**

    https://www.nuget.org/packages/CefSharp.WinForms/
    https://www.nuget.org/packages/CefSharp.Common/
    https://www.nuget.org/packages/cef.redist.x64/

**v79.x** sample :
```js
CefSettings settings = new CefSettings();
settings.UserAgent = General.browser_agent;

settings.CachePath = Application.StartupPath + "\\cache\\";
Directory.CreateDirectory(cache_dir);

settings.PersistSessionCookies = true;

//JS
CefSharpSettings.LegacyJavascriptBindingEnabled = true;
CefSharpSettings.WcfEnabled = true;

//Initialize
Cef.Initialize(settings);

web_view = new ChromiumWebBrowser(General.url);
web_view.FrameLoadEnd += new EventHandler<frameloadendeventargs>(web_view_FrameLoadEnd);
web_view.Dock = DockStyle.Fill;

//JS to NET - https://github.com/cefsharp/CefSharp/issues/2990
web_view.JavascriptObjectRepository.Register("callbackObj", new CallbackObjectForJs(), isAsync: false, options: BindingOptions.DefaultBinder);

panel1.Controls.Add(web_view);

public class CallbackObjectForJs
{
	public void showMessage(string msg)
	{
		MessageBox.Show(msg);		
	}
}
```

* * *

Today tested [EO.Web](https://www.essentialobjects.com/Products/WebBrowser/WinForm.aspx) v2020.1.45 (dependencies = 4 files / 74mb),

EO.WebBrowser dynamically create child processes and run browser engine inside the child process at runtime. By default, Windows system file **rundll32.exe** is used to create the child processes.

here are some snippets :
```js
//set cache - https://www.essentialobjects.com/forum/postsm46061_Cache-Path-solved.aspx
EO.WebBrowser.Runtime.DefaultEngineOptions.CachePath = Application.StartupPath + @"\cache";

webControl1.WebView.Url = "https://www.google.com";

//keyboard hook
webView1.Command += new CommandHandler(WebView_Command);
webView1.Shortcuts = new EO.WebBrowser.Shortcut[]
{
	new EO.WebBrowser.Shortcut(12, EO.WebBrowser.KeyCode.F12, false, false, false),
};

//register JS to .NET handler - https://www.essentialobjects.com/Products/WebBrowser/JSExtension.aspx
webView1.RegisterJSExtensionFunction("callbackObj", new JSExtInvokeHandler(callbackJS));

private void callbackJS(object sender, JSExtInvokeArgs e)
{
	if (e.Arguments!=null)
		your_function(e.Arguments[0].ToString());
}

//keyboard hook
private void WebView_Command(object sender, CommandEventArgs e)
{
	if (e.CommandId == 12)
		EO.WebBrowser.WebView.ShowDebugUI();
}

//inject any JS once the page load completed
private void webView1_LoadCompleted(object sender, EO.WebBrowser.LoadCompletedEventArgs e)
{
	//https://www.essentialobjects.com/doc/webbrowser/advanced/js.aspx
	webView1.EvalScript("alert('hi');");
}
```

* * *

Today tested [Mozilla.Geckofx60.64](https://www.nuget.org/profiles/geckofx) v60.0.50

```js
Xpcom.Initialize(Application.StartupPath + "\\xulrunner"); //x.nupkg\content\Firefox content, copy to app\xulrunner\
Console.Write(Xpcom.ProfileDirectory);
var geckoWebBrowser = new GeckoWebBrowser { Dock = DockStyle.Fill };

this.Controls.Add(geckoWebBrowser);
geckoWebBrowser.Navigate("http://pipiscrew.com/");

/*
howto - https://stackoverflow.com/a/33716554
profile directory - XpCom.ProfileDirectory - https://stackoverflow.com/a/52239283 + https://stackoverflow.com/a/20614986
cookies - https://stackoverflow.com/a/24762756
*/
```</frameloadendeventargs></frameloadendeventargs>

origin - http://www.pipiscrew.com/?p=2454 csharp-cefsharp-hints