---
title: o[nodeJS] Chris Sainty - Remote debug your iisnode hosted nodeJS app
author: PipisCrew
date: 2014-02-15
categories: []
toc: true
---

<span style="color: #ff0000;">**Original article**</span> at [http://blog.csainty.com/2012/03/remote-debug-your-iisnode-hosted-nodejs.html](http://blog.csainty.com/2012/03/remote-debug-your-iisnode-hosted-nodejs.html)

You don’t even need to install the node-inspector package. It is all bundled in with iisnode.
You simply need to make a single change to your web.config rewrite rules so that the urls to launch the debugger are not treated as regular requests and sent through to you app.

```js
<configuration>
  <system.webserver>
    <handlers>
      <add name="iisnode" path="app.js" verb="*" modules="iisnode"></add>
    </handlers>
    <iisnode loggingenabled="false" debuggingenabled="true" debuggerpathsegment="debug"></iisnode>
    <rewrite>
      <rules>
        <clear></clear>
        <rule name="Debug" patternsyntax="Wildcard" stopprocessing="true">
          <match url="app.js/debug*"></match>
          <conditions logicalgrouping="MatchAll" trackallcaptures="false"></conditions>
          <action type="None"></action>
        </rule>
        <rule name="app" patternsyntax="Wildcard">
          <match url="*" negate="false"></match>
          <conditions logicalgrouping="MatchAll" trackallcaptures="false"></conditions>
          <action type="Rewrite" url="app.js"></action>
        </rule>
      </rules>
    </rewrite>
  </system.webserver>
</configuration>
```

So the way you get to the debug console is to hit up /app.js/debug where app.js is the entry point for your app. The rewrite rules here simply allow that url through as it is, everything else gets handed off to the app as normal.

So push up the modified web.config, hit the URL and this nice console pops up.

![](https://www.pipiscrew.com/wp-content/uploads/2014/02/1382874051664.png "1382874051664")

Clicking into Scripts presents you with a list of all the running JavaScript files on the server. Including those built into node itself. You can pick the file you want to debug, and set a break point by clicking on the line numbers.

[![](https://www.pipiscrew.com/wp-content/uploads/2014/02/1382874051665.jpg "1382874051665")](https://www.pipiscrew.com/wp-content/uploads/2014/02/1382874051665.jpg)

With the breakpoint set, now you need to fire a hit off to the website that will run over the breakpoint.

![](https://www.pipiscrew.com/wp-content/uploads/2014/02/1382874051666.png "1382874051666")

This hit will sit there waiting for the server to respond, switch back to your debugger page and the breakpoint has been reached and is waiting for you to take some action.

![](https://www.pipiscrew.com/wp-content/uploads/2014/02/1382874051667.png "1382874051667")

As you can see you have full variable inspection, the options to step through line by line or continue running, variable watch and all the sorts of things you would expect. You even have mouse hover variable inspection like in Visual Studio.

When you are done debugging, you should call the /app.js/debug/?kill url which will shut down the debugger process.

![](https://www.pipiscrew.com/wp-content/uploads/2014/02/1382874051668.png "1382874051668")

Now I wouldn’t go doing this on production, and you certainly do not want to leave that route in place, I would set the debuggingEnabled property to false as well in production but for development or staging servers where you need to follow something through, this is simply awesome.

<span style="color: #ff0000;">**Original article**</span> at [http://blog.csainty.com/2012/03/remote-debug-your-iisnode-hosted-nodejs.html](http://blog.csainty.com/2012/03/remote-debug-your-iisnode-hosted-nodejs.html)

origin - http://www.pipiscrew.com/?p=814 nodejs-chris-sainty-remote-debug-your-iisnode-hosted-nodejs-app