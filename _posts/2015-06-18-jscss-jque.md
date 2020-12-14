---
title: o[js+css] jQuery Animation
author: PipisCrew
date: 2015-06-18
categories: []
toc: true
---

```js

        $("document").ready(function() {
            $("#go").click(function() {
                    $("#testDiv").animate({width: 400})
                    .animate({height: 300}, 400)
                    .animate({left: 200}, 500)
                    .animate({top: "+=100", borderWidth: 10}, "slow")});
        });

<style>
    #testDiv {
        position:relative;
        width: 150px;
        height: 100px;
        margin: 10px;
        padding: 20px;
        background: #b3c8d0;
        border: 1px solid black;
        font-size: 16pt;
        cursor: pointer;
    }
</style>

# Quick jQuery Animation Intro

jQuery provides some basic animation features for showing and hiding elements, as well as a low-level animation function that can be used to animate several CSS properties (as long as they are numeric).

    <button id="go">Go</button>
    <div id="testDiv"></div>

```

scroll from right to left, when stops alert user
```js
//http://api.jquery.com/animate/

var windowWidth = $(window).width()+50;

            $( "#testDiv" ).animate({
                right: windowWidth
              }, 4000, function() {
                  alert("end");
                // Animation complete.
            });

```

origin - http://www.pipiscrew.com/?p=3163 jscss-jquery-animation