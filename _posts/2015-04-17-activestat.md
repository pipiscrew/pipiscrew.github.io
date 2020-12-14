---
title: ActiveState Komodo Edit
author: PipisCrew
date: 2015-04-17
categories: []
toc: true
---

A free, fast and multi-language code editor.

**Download Komodo Edit v9.0.0.15707 freeware for winX86**
[http://downloads.activestate.com/Komodo/releases/9.0.0/Komodo-Edit-9.0.0-15707.msi](http://downloads.activestate.com/Komodo/releases/9.0.0/Komodo-Edit-9.0.0-15707.msi)

or for Linux etc browse at
[http://downloads.activestate.com/Komodo/releases/9.0.0/](http://downloads.activestate.com/Komodo/releases/9.0.0/)

Github :
[http://github.com/Komodo/KomodoEdit](http://github.com/Komodo/KomodoEdit)

Configure on word selection, automatically find highlight all!
You can use it simply by creating new macro (Toolbox -> right mouse click -> Add -> New macro). Then copy-paste this code into it and in "Triggers" tab, check "Macro should trigger on Comodo event" and choose "On startup". Restart Komodo and everything should work just fine.
```js
//source http://community.activestate.com/node/7373
/**
 * Original: http://community.activestate.com/forum/macro-quick-find-highlight#commen...
 * Copyright (c) 2009 Stan Angeloff http://blog.angeloff.name
 *
 * Revision 1: http://code.activestate.com/recipes/577801-quick-find-ctrlf3-on-double-c...
 *   by Adam on 2011-07-22
 * 
 * Revision 2: http://community.activestate.com/node/7373
 *   by peixoto on 2011-10-19
 *
 * Revision 3:
 *   by Furlo on 2012-01-13
 */
if (typeof (extensions) === 'undefined')
  window.extensions = {};

(function() {
  const Cc = Components.classes;
  const Ci = Components.interfaces;

  // Get a reference to the script namespace
  var $self = extensions.findWordUnderCursor ||
              (extensions.findWordUnderCursor = { events: {} });

  // Clean-up after previous execution
  if ($self.onViewClosed)
    window.removeEventListener('view_closed', $self.onViewClosed, false);
  if ($self.onViewOpened)
    window.removeEventListener('view_opened', $self.onViewOpened, false);
  if ($self.destroyAll)
    $self.destroyAll();

  $self.isSupportedView = function(view) {
    return (view && view.getAttribute('type') === 'editor');
  };

  $self.onViewOpened = function(e) {
    var view = e.originalTarget;
    if ($self.isSupportedView(view))
      $self.apply(view);
  };

  $self.onViewClosed = function(e) {
    var view = e.originalTarget;
    if ($self.isSupportedView(view))
      $self.destroy(view);
  };

  $self.destroy = function(view) {
    if (view.uid in $self.events) {
      view.removeEventListener('mouseup', $self.events[view.uid], false);
      delete $self.events[view.uid];
    }
  };

  $self.apply = function(view) {
    var fn = function(e) {
      if (e.which === 1 &&
          !(e.altKey || e.ctrlKey || e.metaKey || e.shiftKey) &&
          !(view.scimoz._startDragDrop || view.scimoz._inDragDrop)) {
        if (view.scimoz.selText.length) {
          e.stopPropagation();
          e.preventDefault();
          $self.jumpToSearch(view);
        }
        else {
          ko.commands.doCommand('cmd_cancel');
        }
      }
    };
    mouseup:view.addEventListener('mouseup', fn, false);
    $self.events[view.uid] = fn;
  };

  window.addEventListener('view_opened', $self.onViewOpened, false);
  window.addEventListener('view_closed', $self.onViewClosed, false);

  $self.forEach = function(fn) {
    var viewsByType = ko.views.manager.topView.getViewsByType(true, 'editor'),
                      view;
    for (var i = 0; i < viewsbytype.length;="" i="" ++)="" {="" view="viewsByType[i];" if="" ($self.issupportedview(view))="" fn.apply($self,="" [view]);="" }="" };="" $self.applytoall="function()" {="" $self.foreach($self.apply);="" };="" $self.destroyall="function()" {="" $self.foreach($self.destroy);="" };="" $self.jumptosearch="function(view)" {="" startline="ko.views.manager.currentView.scimoz.firstVisibleLine;" if="" (ko.views.manager.currentview.scimoz.currentpos="">
        ko.views.manager.currentView.scimoz.anchor) {
      ko.commands.doCommand("cmd_findNextSelected");
      ko.commands.doCommand("cmd_findPrevious");
    }
    else {
      ko.commands.doCommand("cmd_findNextSelected");
    }
    endLine = ko.views.manager.currentView.scimoz.firstVisibleLine;
    changeLine = startLine - endLine;

    //in case it jumps to the top then back in the event that the next
    //selected is at the top of the screen.
    ko.views.manager.currentView.scimoz.lineScroll(0, changeLine); 
  };

  $self.applyToAll();
})();
```

* * *

provide FTP support :

Edit > Preferences > Servers add your server 

![](https://www.pipiscrew.com/wp-content/uploads/2015/04/snap422.png "snap422")

then
![](https://www.pipiscrew.com/wp-content/uploads/2015/04/snap423.png "snap423")

--

for official **Komodo IDE** use **Publising**
[http://docs.activestate.com/komodo/8.5/publish.html](http://docs.activestate.com/komodo/8.5/publish.html)

* * *

> using the default 'Tomorrow Dark' theme, I would like the points that trying to signalize me (aka open/close parenthesis) change textcolor

change also textcolor (aka made white), which I cant find it on Preferences > Color Scheme...
Prefs - Color Scheme - Common Syntax
Element type: bracehighlight

origin - http://www.pipiscrew.com/?p=2833 app-activestate-komodo-edit