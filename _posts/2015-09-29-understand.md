---
title: Understanding ASP.NET View State
author: PipisCrew
date: 2015-09-29
categories: [asp.net]
toc: true
---

[https://msdn.microsoft.com/en-us/library/ms972976.aspx](https://msdn.microsoft.com/en-us/library/ms972976.aspx)

* * *

Global Setting

```js

	<?xml version="1.0"?>

	<configuration>
	    <system.web>
	      <compilation debug="true" targetframework="4.5"></compilation>
	      <httpruntime targetframework="4.5"></httpruntime>
	      <pages enableviewstate="false"></pages>
	    </system.web>
	</configuration>
```

* * *

2nd solution

```js
//on a page, turn EnableViewState false
	<%@ Page Language="C#" EnableViewState="false" AutoEventWireup="true"
	CodeBehind="WebForm1.aspx.cs" Inherits="WebApplication3.WebForm1"  %>
```

* * *

warning the hidden field is always visible even turned OFF!! aka :
```js
<div class="aspNetHidden">
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="heQ5ECpMil93RDNl0WRquLdPfp8pLKaSeDlFfSqq/YDHE0zuDUfpSF0jZnrt+VHecGlOXVoHCpwDpf22i5OQFa0qNgC2aVLp2laM0DJgSoU=">
</div>

```

Beginner's Guide To View State (secure view state)- [http://www.codeproject.com/Articles/31344/Beginner-s-Guide-To-View-State](http://www.codeproject.com/Articles/31344/Beginner-s-Guide-To-View-State)

origin - http://www.pipiscrew.com/?p=2058 understanding-asp-net-view-state