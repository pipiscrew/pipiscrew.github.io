---
title: Easy Native HTML5 Geolocation
author: PipisCrew
date: 2016-01-27
categories: [js]
toc: true
---

```js
//https://gist.github.com/cceremuga/9001819
function successCallback(position) {
    //set latitude / longitude
    var nearLat = position.coords.latitude;
    var nearLong = position.coords.longitude;

    //do whatever you need with the lat / long here
    console.log('Latitude: ' + nearLat + ' Longitude: ' + nearLong);
}

function errorCallback(error) {
    var errorMessage = '';

    switch (error.code) {
        case error.PERMISSION_DENIED:
            errorMessage = "

We cannot find your location. Please make sure location services is enabled then reload the page and click allow when prompted.
"
            break;
        case error.POSITION_UNAVAILABLE:
            errorMessage = "

Location information is unavailable. Please try again later.
"
            break;
        case error.TIMEOUT:
            errorMessage = "

The request to get your location timed out. Please try again later.
"
            break;
        case error.UNKNOWN_ERROR:
            errorMessage = "

An unknown error occurred.
"
            break;
    }

    //do something besides logging this to inform your user what has gone wrong
    console.log(errorMessage);
}

//function to call initially when you want to query lat / long on the device, it calls successCallback on success, errorCallback on error
function getGeoDataFromDevice() {
    //if geo is available, get the current position if the maximum age of the last retrieved position is older than 10 seconds
    if (navigator.geolocation) {
        //high accuracy gets a precise location, but utilizes more battery on a device. We're not doing this excessively, so you should be good to go.
        //Maximum age is "how old can this data be, before we need something fresh" (10 seconds)
        //Timeout is how long should we try to get this information before giving up (20 seconds)
        navigator.geolocation.getCurrentPosition(successCallback, errorCallback, { enableHighAccuracy: true, maximumAge: 10000, timeout: 20000 });
    } else {
        //do something with this besides logging to inform the user their device is unsupported
        console.log('

Your device does not support location detection.
');
    }
}
```

origin - http://www.pipiscrew.com/?p=3449 easy-native-html5-geolocation