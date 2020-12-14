---
title: o[google] Place Autocomplete Address Form
author: PipisCrew
date: 2015-11-09
categories: [js]
toc: true
---

[https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform](https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform)

```js
//source http://stackoverflow.com/a/11577768

var input = document.getElementById('searchTextField');
var options = {
   types: ['(cities)'],
   componentRestrictions: {country: 'gr'} //Greece only
};
var autocomplete = new google.maps.places.Autocomplete(input,options);
```

origin - http://www.pipiscrew.com/?p=2373 google-place-autocomplete-address-form