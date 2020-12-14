---
title: google maps
author: PipisCrew
date: 2016-04-12
categories: [Uncategorized]
toc: true
---

use can use plain anchor like :
```js
http://maps.google.com/?q=38.0868786218,23.8164957270

or

https://www.google.com/maps/place/Athens,Greece
```

you can use **Google Maps JavaScript API**
[http://developers.google.com/maps/documentation/javascript/examples/map-coordinates](http://developers.google.com/maps/documentation/javascript/examples/map-coordinates)

example :
```js

    <style>
      html, body, #map {
        height: 100%;
        margin: 0;
        padding: 0;
      }

    </style>

var marker_map;

    	$(function() {
			var coordinate_map;
			coordinate_map=new google.maps.LatLng(37.8077905, 23.7857412);
			var mapOptions= 
			{
				zoom: 15,
				center: coordinate_map,
				scaleControl: true,
				streetViewControl: false,
				mapTypeControl: false,
				panControl: false,
				zoomControl: true,
				scrollwheel: false,
				zoomControlOptions: {  style: google.maps.ZoomControlStyle.SMALL}, 
				mapTypeControlOptions: { mapTypeIds: [google.maps.MapTypeId.ROADMAP, 'map_style'] }
			}; 

			var styles = [	{	"stylers": [{"saturation": -100	}]	}	];

			var styledMap = new google.maps.StyledMapType(styles, {name: "Styled Map"});
			var map = new google.maps.Map(document.getElementById('map'),mapOptions);
			map.mapTypes.set('map_style', styledMap);
			map.setMapTypeId('map_style');

			//use of public variable - the marker itself
			marker_map = new google.maps.Marker({
					position: new google.maps.LatLng(37.8077905, 23.7857412),
					animation:  google.maps.Animation.DROP,
					map: map,
					icon: 'marker.png'
				});

			//---------------------------when marker clicked #bounce#
			//use of public variable
			google.maps.event.addListener(marker_map, 'click', toggleBounce);
			//---------------------------when marker clicked #bounce#

				//button click
				$('#btn').on('click', function(e) {
						var allLocs = [{"lat":"37.9060197527","lng":"23.7515864000"},{"lat":"37.8605266640","lng":"23.7554984730"},{"lat":"38.0868786218","lng":"23.8164957270"},{"lat":"37.9772695000","lng":"23.7368496000"},{"lat":"37.9777561860","lng":"23.7425824577"},{"lat":"37.9477112582","lng":"23.7150144270"},{"lat":"37.9674859000","lng":"23.7492797000"},{"lat":"37.9634163000","lng":"23.7249817000"},{"lat":"38.0304100169","lng":"23.8020953693"},{"lat":"38.0196767696","lng":"23.7942414914"},{"lat":"37.9992306362","lng":"23.7707444847"},{"lat":"38.0038740823","lng":"23.7753516921"}];
						var i = new google.maps.LatLng(37.8077905, 23.7857412)

						var e = document.getElementById("map");
				        var o = {
				            center: i,
				            zoom: 11,
				            mapTypeId: google.maps.MapTypeId.ROADMAP
				        };
				        var map = new google.maps.Map(e, o);
				        var panLeft = -350;

					    for (var r in allLocs) {
					        var s = allLocs[r].lat,
					            l = allLocs[r].lng;
					        ll = new google.maps.LatLng(s, l), marker = new google.maps.Marker({
					            position: ll,
					            map: map,
					            icon: "marker2.png"
					        })
					    }
					    map.panBy(panLeft, -160)
				});

		})//jQ

		//use of public variable
		function toggleBounce() {
		  if (marker_map.getAnimation() != null) {
			marker_map.setAnimation(null);
		  } else {
			marker_map.setAnimation(google.maps.Animation.BOUNCE);
		  }
		}

		<button id="btn">
			Add more markers
		</button>
    <div id="map"></div>

```

![](https://www.pipiscrew.com/wp-content/uploads/2015/07/marker.png "marker")

![](https://www.pipiscrew.com/wp-content/uploads/2015/07/marker2.png "marker2")

* * *

> find by address, not by LatLng

reference - [http://developers.google.com/apps-script/reference/maps/geocoder](http://developers.google.com/apps-script/reference/maps/geocoder)
```js
//geocoder test - source http://stackoverflow.com/a/15928376

    <style>
      #map-canvas {
        width: 500px;
        height: 400px;
      }
    </style>

		var geocoder;

	  var address ="Greece, Athens";

      function initialize() {
	  geocoder = new google.maps.Geocoder();

        var mapCanvas = document.getElementById('map-canvas');
        var mapOptions = {
          zoom: 8,
          mapTypeId: google.maps.MapTypeId.ROADMAP
        }
        var map = new google.maps.Map(mapCanvas, mapOptions)

		if (geocoder) {
			  geocoder.geocode( { 'address': address}, function(results, status) {
				if (status == google.maps.GeocoderStatus.OK) {
				  if (status != google.maps.GeocoderStatus.ZERO_RESULTS) {
				  map.setCenter(results[0].geometry.location);

					var infowindow = new google.maps.InfoWindow(
						{ content: '**'+address+'**',
						  size: new google.maps.Size(150,50)
						});

					var marker = new google.maps.Marker({
						position: results[0].geometry.location,
						map: map, 
						title:address
					}); 
					google.maps.event.addListener(marker, 'click', function() {
						infowindow.open(map,marker);
					});

				  } else {
					alert("No results found");
				  }
				} else {
				  alert("Geocode was not successful for the following reason: " + status);
				}
			  });
			}

      }
      google.maps.event.addDomListener(window, 'load', initialize);

    <div id="map-canvas"></div>

```

* * *

> find by address minimal, with custom marker info

```js
//sarantis.html

<div id="map" style="width:100%; height:400px;"></div>

    function initMap() {
        jQuery.ajax({
            url: "https://maps.googleapis.com/maps/api/geocode/json?&address=Αλαμάνας 1 και Πρεμετής, 151 25",
            success: function(result) {
                var lattitude = result.results[0].geometry.location.lat;
                var longitute = result.results[0].geometry.location.lng;

                var place = {
                    lat: lattitude,
                    lng: longitute
                };
                var map = new google.maps.Map(document.getElementById('map'), {
                    zoom: 16,
                    center: place
                });

                var contentString = '<div id="content" style="overflow:hidden; text-align:center; vertical-align:middle">' +
                    '

#### Test @ PipisCrew

' +
                    '<div id="bodyContent" style="margin: 2px auto; padding-top: 2px; font-size: 14px; line-height: 16px;">' +
                    '

Αλαμάνας 1 και Πρεμετής, 15125
' +
                    '

Τηλέφωνο : x, x
' +
                    '

e-mail : <a href="mailto:x@x.com">x@x.com</a>
' +
                    '</div>' +
                    '</div>';

                var infowindow = new google.maps.InfoWindow({
                    content: contentString
                });

                var marker = new google.maps.Marker({
                    position: place,
                    map: map,
                    title: 'Test @ PipisCrew'
                });
                marker.addListener('click', function() {
                    infowindow.open(map, marker);
                });
            }
        });

    }

```

[http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)
async downloads the file during HTML parsing and will pause the HTML parser to execute it when it has finished downloading.
defer downloads the file during HTML parsing and will only execute it after the parser has completed. defer scripts are also guarenteed to execute in the order that they appear in the document.

origin - http://www.pipiscrew.com/?p=3383 js-google-maps