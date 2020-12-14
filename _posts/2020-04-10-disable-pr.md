---
title: Disable processor boost mode
author: PipisCrew
date: 2020-04-10
categories: [news]
toc: true
---

However, boost mode also drains the battery quicker and can bring up the device temperature. In small contained devices with poor heat exchange (like most laptops), this will spin up the fans but the temperature will also raise. A rise in processor temperature will also lead to increased temperatures in other components including the battery.

Disable boost mode and sacrifices some peak performance in exchange for a cooler laptop and prolonged battery life.

The temperature change you’ll see by disabling boost mode will vary based on your environment, hardware, and usage pattern. His MacBook Pro dropped the average battery temperature from 41℃ to 32℃ after disabling boost mode. It also runs quieter and the battery last about 30 % longer on a charge.

Execute 
```js
powercfg.exe -attributes sub_processor perfboostmode -attrib_hide
```

this will make **visible** the option **Performance Boost Mode** under **Processor power management**

![](https://i.imgur.com/XSSxheT.jpg)

from there set the **OnBattery** & **Pluggedin** to **disabled**. No restart needed.

src - https://www.ctrl.blog/entry/laptop-boost-mode-battery.html

> If you have enabled virtualization in your BIOS or UEFI settings, then Processor power management will not be available, even if you set them to be added.
> 
> Only when virtualization is disabled in BIOS/UEFI will be shown

[src](https://www.eightforums.com/threads/power-options-add-or-remove-min-max-processor-state.51027/)

* * *

Many other factors can affect device temperatures. **Poor ventilation** is a primary cause of hot laptops. You can improve the ventilation by applying floor protectors to the bottom of your laptop to create more clearing between it and the table. There’s absolutely no need to buy an expensive cooling stand for your laptop. 

The instructions are super simple:

1-Pick up some thick, round, and medium-sized felt pads or anti-slip pads
2-Cut one pad along the middle using scissors
3-Glue one half on either side with the round end pointing backward and the straight edge facing forward on the underside of your the laptop towards the back (pictured below)

This will lift the laptop slightly higher off the resting surface on the table. This will allow for heat exhausted from the laptop to dissipate faster due to the increased space making room for more air circulation. It’s an easy way to improve laptop cooling.

src - https://www.ctrl.blog/entry/how-to-laptop-air-cooling-pads.html

ref
https://www.amazon.co.uk/s?k=floor+protector+felt+pads
https://www.amazon.co.uk/s?k=floor+protector+anti-slip+pads

origin - https://www.pipiscrew.com/?p=18019 disable-processor-boost-mode