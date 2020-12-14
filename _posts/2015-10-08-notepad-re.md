---
title: o[notepad++] Remove lines containing
author: PipisCrew
date: 2015-10-08
categories: [fun]
toc: true
---

reference 
[http://stackoverflow.com/a/19386617](http://stackoverflow.com/a/19386617)

## solution 1

Find what:
```js
.*help.*\r?\n
```

Replace with: text box empty.

Make sure the Regular expression radio button in the Search Mode area is selected. Then click Replace All and voila! 

## solution 2

Is also possible with Notepad++

Goto the search menu **Ctrl+F** and there to the **"Mark" tab**. Check **"Bookmark
line"** (if there is no "Mark" tab update to the current version).

Then just enter your search term and click **"Mark All"**

==> All line containing the search term are bookmarked.

Now go to the Menu **"Search -> Bookmark -> Remove Bookmarked lines"**

origin - http://www.pipiscrew.com/?p=2124 notepad-remove-lines-containing