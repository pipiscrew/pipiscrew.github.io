---
title: Slack Disable WYSIWYG Bookmarklet
author: PipisCrew
date: 2019-11-21
categories: [js]
toc: true
---

src - https://github.com/kfahy/slack-disable-wysiwyg-bookmarklet

```js
javascript:(_ => {
  const redux = slackDebug[slackDebug.activeTeamId].redux;
  const {wysiwyg_composer, wysiwyg_composer_ios, wysiwyg_composer_webapp, ...payload} = redux.getState().experiments;
  redux.dispatch({ type: '[19] Bulk add experiment assignments to redux', payload });
})();
```

origin - https://www.pipiscrew.com/?p=15863 slack-disable-wysiwyg-bookmarklet