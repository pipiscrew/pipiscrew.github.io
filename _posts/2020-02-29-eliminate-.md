---
title: Eliminate Windows 10 telemetry
author: PipisCrew
date: 2020-02-29
categories: [news]
toc: true
---

As per [Debloat-Windows-10](https://github.com/W4RH4WK/Debloat-Windows-10) **block-telemetry.ps1**, better download the archive contains more tweaks.

merge this to C:\Windows\System32\drivers\etc\**hosts** file

[code]
0.0.0.0 184-86-53-99.deploy.static.akamaitechnologies.com
0.0.0.0 a-0001.a-msedge.net
0.0.0.0 a-0002.a-msedge.net
0.0.0.0 a-0003.a-msedge.net
0.0.0.0 a-0004.a-msedge.net
0.0.0.0 a-0005.a-msedge.net
0.0.0.0 a-0006.a-msedge.net
0.0.0.0 a-0007.a-msedge.net
0.0.0.0 a-0008.a-msedge.net
0.0.0.0 a-0009.a-msedge.net
0.0.0.0 a1621.g.akamai.net
0.0.0.0 a1856.g2.akamai.net
0.0.0.0 a1961.g.akamai.net
0.0.0.0 a978.i6g1.akamai.net
0.0.0.0 a.ads1.msn.com
0.0.0.0 a.ads2.msads.net
0.0.0.0 a.ads2.msn.com
0.0.0.0 ac3.msn.com
0.0.0.0 ad.doubleclick.net
0.0.0.0 adnexus.net
0.0.0.0 adnxs.com
0.0.0.0 ads1.msads.net
0.0.0.0 ads.msn.com
0.0.0.0 aidps.atdmt.com
0.0.0.0 aka-cdn-ns.adtech.de
0.0.0.0 any.edge.bing.com
0.0.0.0 a.rad.msn.com
0.0.0.0 az361816.vo.msecnd.net
0.0.0.0 az512334.vo.msecnd.net
0.0.0.0 b.ads1.msn.com
0.0.0.0 b.ads2.msads.net
0.0.0.0 bingads.microsoft.com
0.0.0.0 b.rad.msn.com
0.0.0.0 bs.serving-sys.com
0.0.0.0 c.atdmt.com
0.0.0.0 cdn.atdmt.com
0.0.0.0 cds26.ams9.msecn.net
0.0.0.0 choice.microsoft.com
0.0.0.0 choice.microsoft.com.nsatc.net
0.0.0.0 compatexchange.cloudapp.net
0.0.0.0 corpext.msitadfs.glbdns2.microsoft.com
0.0.0.0 corp.sts.microsoft.com
0.0.0.0 cs1.wpc.v0cdn.net
0.0.0.0 db3aqu.atdmt.com
0.0.0.0 df.telemetry.microsoft.com
0.0.0.0 diagnostics.support.microsoft.com
0.0.0.0 e2835.dspb.akamaiedge.net
0.0.0.0 e7341.g.akamaiedge.net
0.0.0.0 e7502.ce.akamaiedge.net
0.0.0.0 e8218.ce.akamaiedge.net
0.0.0.0 ec.atdmt.com
0.0.0.0 fe2.update.microsoft.com.akadns.net
0.0.0.0 feedback.microsoft-hohm.com
0.0.0.0 feedback.search.microsoft.com
0.0.0.0 feedback.windows.com
0.0.0.0 flex.msn.com
0.0.0.0 g.msn.com
0.0.0.0 h1.msn.com
0.0.0.0 h2.msn.com
0.0.0.0 hostedocsp.globalsign.com
0.0.0.0 i1.services.social.microsoft.com
0.0.0.0 i1.services.social.microsoft.com.nsatc.net
0.0.0.0 ipv6.msftncsi.com
0.0.0.0 ipv6.msftncsi.com.edgesuite.net
0.0.0.0 lb1.www.ms.akadns.net
0.0.0.0 live.rads.msn.com
0.0.0.0 m.adnxs.com
0.0.0.0 msnbot-65-55-108-23.search.msn.com
0.0.0.0 msntest.serving-sys.com
0.0.0.0 oca.telemetry.microsoft.com
0.0.0.0 oca.telemetry.microsoft.com.nsatc.net
0.0.0.0 onesettings-db5.metron.live.nsatc.net
0.0.0.0 pre.footprintpredict.com
0.0.0.0 preview.msn.com
0.0.0.0 rad.live.com
0.0.0.0 redir.metaservices.microsoft.com
0.0.0.0 reports.wes.df.telemetry.microsoft.com
0.0.0.0 schemas.microsoft.akadns.net
0.0.0.0 secure.adnxs.com
0.0.0.0 secure.flashtalking.com
0.0.0.0 services.wes.df.telemetry.microsoft.com
0.0.0.0 settings-sandbox.data.microsoft.com
0.0.0.0 sls.update.microsoft.com.akadns.net
0.0.0.0 sqm.df.telemetry.microsoft.com
0.0.0.0 sqm.telemetry.microsoft.com
0.0.0.0 sqm.telemetry.microsoft.com.nsatc.net
0.0.0.0 ssw.live.com
0.0.0.0 static.2mdn.net
0.0.0.0 statsfe1.ws.microsoft.com
0.0.0.0 statsfe2.update.microsoft.com.akadns.net
0.0.0.0 statsfe2.ws.microsoft.com
0.0.0.0 survey.watson.microsoft.com
0.0.0.0 telecommand.telemetry.microsoft.com
0.0.0.0 telecommand.telemetry.microsoft.com.nsatc.net
0.0.0.0 telemetry.appex.bing.net
0.0.0.0 telemetry.urs.microsoft.com
0.0.0.0 vortex-bn2.metron.live.com.nsatc.net
0.0.0.0 vortex-cy2.metron.live.com.nsatc.net
0.0.0.0 vortex.data.microsoft.com
0.0.0.0 vortex-sandbox.data.microsoft.com
0.0.0.0 vortex-win.data.microsoft.com
0.0.0.0 cy2.vortex.data.microsoft.com.akadns.net
0.0.0.0 watson.live.com
0.0.0.0 watson.ppe.telemetry.microsoft.com
0.0.0.0 watson.telemetry.microsoft.com
0.0.0.0 watson.telemetry.microsoft.com.nsatc.net
0.0.0.0 win10.ipv6.microsoft.com
0.0.0.0 www.bingads.microsoft.com
0.0.0.0 www.go.microsoft.akadns.net
0.0.0.0 www.msftncsi.com
0.0.0.0 client.wns.windows.com
0.0.0.0 wdcpalt.microsoft.com
0.0.0.0 settings-ssl.xboxlive.com
0.0.0.0 settings-ssl.xboxlive.com-c.edgekey.net
0.0.0.0 settings-ssl.xboxlive.com-c.edgekey.net.globalredir.akadns.net
0.0.0.0 e87.dspb.akamaidege.net
0.0.0.0 insiderservice.microsoft.com
0.0.0.0 insiderservice.trafficmanager.net
0.0.0.0 e3843.g.akamaiedge.net
0.0.0.0 flightingserviceweurope.cloudapp.net
0.0.0.0 static.ads-twitter.com
0.0.0.0 www-google-analytics.l.google.com
0.0.0.0 p.static.ads-twitter.com
0.0.0.0 hubspot.net.edge.net
0.0.0.0 e9483.a.akamaiedge.net
0.0.0.0 stats.g.doubleclick.net
0.0.0.0 stats.l.doubleclick.net
0.0.0.0 adservice.google.de
0.0.0.0 adservice.google.com
0.0.0.0 googleads.g.doubleclick.net
0.0.0.0 pagead46.l.doubleclick.net
0.0.0.0 hubspot.net.edgekey.net
0.0.0.0 insiderppe.cloudapp.net
0.0.0.0 livetileedge.dsx.mp.microsoft.com
0.0.0.0 s0.2mdn.net
0.0.0.0 view.atdmt.com
0.0.0.0 m.hotmail.com
0.0.0.0 apps.skype.com
0.0.0.0 c.msn.com
0.0.0.0 pricelist.skype.com
0.0.0.0 s.gateway.messenger.live.com
0.0.0.0 ui.skype.com
[/code]

execute powershell with admin privileges, first enable the execution
```js
Set-ExecutionPolicy Unrestricted
```

dump these to a **test.ps1** file, save & execute it (without quotes) via "./test.ps1"
```js
Write-Output "Adding telemetry ips to firewall"
$ips = @(
    "134.170.30.202"
    "137.116.81.24"
    "157.56.106.189"
    "184.86.53.99"
    "2.22.61.43"
    "2.22.61.66"
    "204.79.197.200"
    "23.218.212.69"
    "65.39.117.230"
    "65.52.108.33"   # Causes problems with Microsoft Store
    "65.55.108.23"
    "64.4.54.254"
)
Remove-NetFirewallRule -DisplayName "Block Telemetry IPs" -ErrorAction SilentlyContinue
New-NetFirewallRule -DisplayName "Block Telemetry IPs" -Direction Outbound `
    -Action Block -RemoteAddress ([string[]]$ips)

```

origin - https://www.pipiscrew.com/?p=17230 eliminate-windows-10-telemetry