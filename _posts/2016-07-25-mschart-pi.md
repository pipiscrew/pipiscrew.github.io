---
title: MSChart- Pie Chart Label Overlapping
author: PipisCrew
date: 2016-07-25
categories: [.net]
toc: true
---

[http://stackoverflow.com/questions/10497392/mschart-pie-chart-label-overlapping-issue](http://stackoverflow.com/questions/10497392/mschart-pie-chart-label-overlapping-issue)

```js
Chart1.Series[0]["PieLabelStyle"] = "Outside";
Chart1.ChartAreas[0].Area3DStyle.Enable3D = true;
Chart1.ChartAreas[0].Area3DStyle.Inclination = 10;
```

origin - http://www.pipiscrew.com/?p=5930 mschart-pie-chart-label-overlapping