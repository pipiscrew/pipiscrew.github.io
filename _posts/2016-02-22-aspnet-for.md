---
title: o[asp.net] Form Submit UpdateProgress
author: PipisCrew
date: 2016-02-22
categories: [asp.net]
toc: true
---

references
[http://stackoverflow.com/a/7708659](http://stackoverflow.com/a/7708659)
[http://preloaders.net/](http://preloaders.net/)

just include the following code snippet into a form tag aka ```js<form></form>```

## using Image as Loading

```js
<asp:updateprogress id="updateProgress" runat="server">
    <progresstemplate>
        <div style="position: fixed; text-align: center; height: 100%; width: 100%; top: 0; right: 0; left: 0; z-index: 9999999; background-color: #000000; opacity: 0.7;">
            <asp:image id="imgUpdateProgress" runat="server" imageurl="~/images/ajax-loader.gif" alternatetext="Loading ..." tooltip="Loading ..." style="padding: 10px;position:fixed;top:45%;left:50%;"></asp:image>
        </div>
    </progresstemplate>
</asp:updateprogress>
```

## using Text as Loading

```js
<asp:updateprogress id="updateProgress" runat="server">
    <progresstemplate>
        <div style="position: fixed; text-align: center; height: 100%; width: 100%; top: 0; right: 0; left: 0; z-index: 9999999; background-color: #000000; opacity: 0.7;">
            <span style="border-width: 0px; position: fixed; padding: 50px; background-color: #FFFFFF; font-size: 36px; left: 40%; top: 40%;">Loading ...</span>
        </div>
    </progresstemplate>
</asp:updateprogress>
```

origin - http://www.pipiscrew.com/?p=3941 asp-net-form-submit-updateprogress