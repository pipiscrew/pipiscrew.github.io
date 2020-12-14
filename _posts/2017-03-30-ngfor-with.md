---
title: ngFor with service
author: PipisCrew
date: 2017-03-30
categories: [angular]
toc: true
---

```js
//x.component.html

*   ![]({{item.url_t}})

<button type="button" (click)="callFlickr()">Get new images!</button>

//flickr.service.ts
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';
import 'rxjs/Rx';

@Injectable()
export class FlickrService {
constructor (private http: Http) {}

public getImages() {
        return this.http.post("https://api.flickr.com/services/rest/?method=flickr.photos.getRecent&per_page=5&format=json&nojsoncallback=1&extras=url_t&api_key=0eb28a07a69f09f148ce289", "");
    }

}

//x.component.ts
import { Component } from '@angular/core';
import { FlickrService } from './flickr.service';

export class AppComponent {
  private flickrOBJ: any[] = []; // the ngFor tied with the array

  constructor(private flickrService: FlickrService) { }

    callFlickr() {
        this.flickrService.getImages().subscribe((data) => {
                                                                console.log(JSON.parse(data['_body']).photos.photo);
                                                                this.flickrOBJ = (JSON.parse(data['_body']).photos.photo);
                                                            }, (err) => console.log("error occured", err));

    }
}
```

origin - http://www.pipiscrew.com/?p=7420 ngfor-with-service