---
title: get sender obj by event
author: PipisCrew
date: 2014-12-18
categories: []
toc: true
---

reference 
[http://javascript.info/tutorial/obtaining-event-object](http://javascript.info/tutorial/obtaining-event-object)

> The event object is always passed to the handler and contains a lot of useful information what has happened.

various line will be something like :
onclick='javascript:test("999",**event**)'

the **event** object doesnt exist in my code structure, browsers which follow W3C standards always pass the **event** object!

```js

.
.
.

	function fill_list(db)
		for (var i = 0; i < db.length;="" i++)="" {="" rows="" +="<tr><td></td><td>" +="" db[i]["offer_id"]="" +=""><td>" +
			"<a id='" + db[i]["offer_id"] + "' onclick='test(" + db[i]["offer_id"] + ",event)' class='btn btn-danger btn-xs'>Mark as Paid</a></td>";
		}

		$("#table").html(rows);
	}

	function test(offer_id,eventt){
		console.log(eventt);
		var t = eventt.srcElement;
		console.log(t);

		//get ID by sender!
		$("#"+t.id).hide();
	}

[/javascript]

at first 
![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap331.png "snap331")

at second (when user clicked the red button)
![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap331b.png "snap331b")

![](https://www.pipiscrew.com/wp-content/uploads/2014/12/snap333.png "snap333")
1-console.log(eventt)
2-console.log(eventt.srcElement)

origin - http://www.pipiscrew.com/?p=2100 js-get-sender-obj-by-event