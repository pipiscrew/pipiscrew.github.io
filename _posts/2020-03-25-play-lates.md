---
title: play latest music releases online
author: PipisCrew
date: 2020-03-25
categories: [news]
toc: true
---

source - [http://bigup2dance.tumblr.com/post/102614949869/hacker-advice-to-djs-listen-before-you-buy](http://bigup2dance.tumblr.com/post/102614949869/hacker-advice-to-djs-listen-before-you-buy)

Go to [http://redeyerecords.co.uk](http://redeyerecords.co.uk)

Click on a genre of your choice.
Press ctrl + shift + k (or j in chrome) to get the web console available.

Paste this:
```js
var releases = document.getElementsByClassName("sfPlay");
for(var i = 0; i < releases.length;="" i++)="" {="" var="" redid="releases[i].id.substr(1);" console.log("http://cdn.redeyerecords.co.uk/"="" +="" redid="" +="" ".mp3");="" }="" ```="" in="" the="" console="" you="" will="" get="" a="" list="" of="" all="" mp3s="" visible="" on="" the="" site.="" download="" them="" and="" start="" practicing.="" to="" do="" the="" same="" at="">[http://toolboxrecords.com](http://toolboxrecords.com) get to your preferred genre section and paste this in to your JavaScript console:

```js
var releases = document.querySelectorAll(".track-title[rel]");
for(var i = 0; i < releases.length; i++)
   console.log(producttrackurl + "/" + releases[i].getattribute("rel"));
```

here is a list of all the latest tunes for your enjoyment in low quality cut up so they don’t take forever to browse. do not play these mp3 files live releases.length;="" i++)="" console.log(producttrackurl="" +="" "/"="" +="" releases[i].getattribute("rel"));="" ```="" here="" is="" a="" list="" of="" all="" the="" latest="" tunes="" for="" your="" enjoyment="" in="" low="" quality="" cut="" up="" so="" they="" don’t="" take="" forever="" to="" browse.="" do="" not="" play="" these="" mp3="" files=""></ releases.length; i++)
   console.log(producttrackurl + "/" + releases[i].getattribute("rel"));
```

here is a list of all the latest tunes for your enjoyment in low quality cut up so they don’t take forever to browse. do not play these mp3 files live>

origin - http://www.pipiscrew.com/?p=5090 play-latest-releases-online