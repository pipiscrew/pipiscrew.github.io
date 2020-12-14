---
title: o[chrome] Stylebot
author: PipisCrew
date: 2015-08-29
categories: [app]
toc: true
---

[https://chrome.google.com/webstore/detail/stylebot/oiaejidbmkiecgbjeifoejpgmdaleoha](https://chrome.google.com/webstore/detail/stylebot/oiaejidbmkiecgbjeifoejpgmdaleoha)

source [http://atom0s.com/forums/viewtopic.php?t=80](http://atom0s.com/forums/viewtopic.php?t=80)

Next follow these short steps to block the needed parts of the Google News page:

*   Open Stylebot's options by clicking on the added button the extension made and choose 'Options' from the dropdown.

*   Once the options are open, click on the 'Styles' link on the left side.

*   Then on the right side, click 'Add a new style...'.

*   For the url, enter: news.google.com

*   For the CSS override in the bottom box, enter:

```js
div.section.top-stories-section.section-toptop {
    display: none;
}

li.nav-item.nv-FRONTPAGE.selected-nav-item.topic-nav-item {
    display: none;
}
```

origin - http://www.pipiscrew.com/?p=1746 chrome-stylebot