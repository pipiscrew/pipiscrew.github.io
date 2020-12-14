---
title: JavaScript engines
author: PipisCrew
date: 2015-09-23
categories: [js,news]
toc: true
---

While keeping in mind the heavy marketing influence in naming and renaming these engines, it’s useful to note a few of the major events in the history of the JavaScript engine. I’ve compiled a handy chart for you:
<table id="engines" cellspacing="0" cellpadding="0">
<thead>
<tr>
<th>Browser, Headless Browser, or Runtime</th>
<th>JavaScript Engine</th>
</tr>
</thead>
<tbody>
<tr>
<td>Mozilla</td>
<td>Spidermonkey</td>
</tr>
<tr>
<td>Chrome</td>
<td>V8</td>
</tr>
<tr>
<td>Safari**</td>
<td>JavaScriptCore*</td>
</tr>
<tr>
<td>IE and Edge</td>
<td>Chakra</td>
</tr>
<tr>
<td>PhantomJS</td>
<td>JavaScriptCore</td>
</tr>
<tr>
<td>HTMLUnit</td>
<td>Rhino</td>
</tr>
<tr>
<td>TrifleJS</td>
<td>V8</td>
</tr>
<tr>
<td>Node.js***</td>
<td>V8</td>
</tr>
<tr>
<td>Io.js***</td>
<td>V8</td>
</tr>
</tbody>
</table>
*JavaScriptCore was rewritten as SquirrelFish, rebranded as SquirrelFish Extreme also called Nitro. It’s still a true statement however to call JavaScriptCore the JavaScript engine that underlies WebKit implementations (such as Safari).

**iOS developers should be aware that Mobile Safari leverages Nitro, but UIWebView does not include JIT compilation, so the experience is slower. With iOS8, however, developers can use [WKWebView](http://developer.telerik.com/featured/why-ios-8s-wkwebview-is-a-big-deal-for-hybrid-development/) which includes access to Nitro, speeding up the experience [considerably](http://devgirl.org/2014/11/10/boost-your-ios-8-mobile-app-performance-with-wkwebview/). Hybrid mobile app developers should be able to breathe a little easier.

***One of the factors in the decision to split io.js from Node.js had to do with the version of V8 that would be supported by the project. This continues to be a challenge, as outlined [here](https://medium.com/node-js-javascript/4-0-is-the-new-1-0-386597a3436d).

source [http://developer.telerik.com/featured/a-guide-to-javascript-engines-for-idiots/](http://developer.telerik.com/featured/a-guide-to-javascript-engines-for-idiots/)

origin - http://www.pipiscrew.com/?p=2024 javascript-engines