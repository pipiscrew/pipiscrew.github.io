---
title: o[firebase] query by priority
author: PipisCrew
date: 2017-02-26
categories: [news]
toc: true
---

**references :**

[https://www.firebase.com/blog/2013-10-01-queries-part-one.html](https://www.firebase.com/blog/2013-10-01-queries-part-one.html)

[https://www.firebase.com/blog/2014-01-02-queries-part-two.html](https://www.firebase.com/blog/2014-01-02-queries-part-two.html)

[https://www.firebase.com/docs/javascript/query/startat.html](https://www.firebase.com/docs/javascript/query/startat.html)

[https://www.firebase.com/docs/javascript/firebase/endat.html](https://www.firebase.com/docs/javascript/firebase/endat.html)

**example by kato** 

[http://jsfiddle.net/katowulf/vQEmt/2/](http://jsfiddle.net/katowulf/vQEmt/2/)

where at firebase

![](https://www.pipiscrew.com/wp-content/uploads/2014/01/snap548.png "snap548")

*******************************************************************

startAt + endAt uses .priority field to query the nodes, firstly I used to store the dateCreated to .priority... great then at code with just a .startAt, I grab the needed...

Later, a need occurred, to list the nodes also via another field, contacted firebase support the reply was :

> few different approaches here:
> 
> 1) Merge category and priority into one string and set that as the priority of the records
> 
> 2) Create an [index ](http://zenovations.github.io/FirebaseIndex/)of records by category and iterate that list to grab them by ID.
> 
> 3) Try ElasticSearch, which is nearly plug-and-play with Firebase, to look up records by complex criteria. [Check out our blog post on this](https://www.firebase.com/blog/2014-01-02-queries-part-two.html).

ok, I proceed with 1) so now, I have something like :

![](https://www.pipiscrew.com/wp-content/uploads/2014/01/snap549.png "snap549")

so I started to make examples to understand how works, the need is to list [from - to] period + specific country :

```js
*1*
    .startAt('Afghanistan')
    .endAt('Afghanistan');

//no result

*2*
    .startAt('Afghanistan1390383000')
    .endAt('Afghanistan1390383000');

//I got 1row

*3*
    .startAt('Afghanistan1190383000')
    .endAt('Afghanistan1290383000');

//no result

*4*
    .startAt('Afghanistan1290383000')
    .endAt('Afghanistan1390383000');

//I got 1row

*5*
    .startAt('Afghanistan1290383000')
    .endAt('Afghanistan1390382000'); //the last 3000 to 2000

//no result
```

conclusion store first the text field then the UTC, the previous queries saw us that can handle the alphanumeric using startAt and endAt!

origin - http://www.pipiscrew.com/?p=727 firebase-query-by-priority