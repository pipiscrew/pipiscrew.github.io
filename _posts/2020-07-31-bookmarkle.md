---
title: Bookmarklet - Google translate
author: PipisCrew
date: 2020-07-31
categories: [js]
toc: true
---

With no selected text the whole page is opened in Google Translate.When there is selected text only this text snippet is sent to Google Translate. http is working you can change it to https if you like.

```js
javascript:var%20t=((window.getSelection&&window.getSelection())||(document.getSelection&&document.getSelection())||(document.selection&&document.selection.createRange&&document.selection.createRange().text));var%20e=(document.charset||document.characterSet);if(t!=''){location.href='http://translate.google.com/translate_t?text='+t+'&hl=en&langpair=auto|en&tbb=1&ie='+e;}else{location.href='http://translate.google.com/translate?u='+escape(location.href)+'&hl=en&langpair=auto|en&tbb=1&ie='+e;};
```

src - https://www.ghacks.net/2020/07/31/translate-selected-text-quickly-with-the-simple-translate-extension-for-chrome-and-firefox/

alternative Google addon
https://chrome.google.com/webstore/detail/simple-translate/ibplnjkanclpjokhdolnendpplpjiace

origin - https://www.pipiscrew.com/?p=18763 bookmarklet-google-translate