---
title: TRULY Understanding Webforms ViewState
author: PipisCrew
date: 2020-09-14
categories: [asp.net]
toc: true
---

https://weblogs.asp.net/infinitiesloop/Truly-Understanding-Viewstate

WHAT DOES VIEWSTATE DO?
-Stores values per control by key name, like a Hashtable
-Tracks changes to a ViewState value's initial state
-Serializes and Deserializes saved data into a hidden form field on the client
-Automatically restores ViewState data on postbacks

WHAT DOESN'T VIEWSTATE DO?
-Automatically retain state of class variables (private, protected, or public)
-Remember any state information across page loads (only postbacks) (that is unless you customize how the data is persisted)
-Remove the need to repopulate data on every request
-ViewState is not responsible for the population of values that are posted such as by TextBox controls (although it does play an important role)
-Make you coffee

origin - https://www.pipiscrew.com/?p=19068 truly-understanding-webforms-viewstate