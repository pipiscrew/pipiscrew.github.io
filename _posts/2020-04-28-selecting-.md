---
title: Selecting multiple elements with the same id using querySelectorAll and use the returned nodelist object
author: PipisCrew
date: 2020-04-28
categories: [js]
toc: true
---

![](https://i.imgur.com/bQqekvd.png)
The **querySelectorAll**, return the select items as **Nodelist object**. NodeList is not an Array, it is possible to iterate on it using **forEach**(). It can also be converted to an Array using Array.from(). ([more](https://developer.mozilla.org/en-US/docs/Web/API/NodeList))

### Trigger the event
![](https://i.imgur.com/WjhPmli.png)

the **e**, is the mouse event, to get the actual 'source' element that clicked we use **e.srcElement**

![](https://i.imgur.com/tXdUcqW.png)

to get the parent, we using the **e.srcElement.parentNode**

![](https://i.imgur.com/dPvzQHv.png)

* * *

Put it all together

```js
//example of TR

<tr class="topics">

<td>  //first TD
		![](assets/cat_icon.png)
	</td>

<td>  //second TD
		[Health](list_topics.php?id=1)
	</td>

<td>2018-06-04</td>

<td>
		<span class="glyphicon glyphicon-ok"></span>
	</td>

<td>  //fourth TD
		[Edit]()
	</td>

</tr>

```

![](https://i.imgur.com/yUMcTUY.png)

```js
var tbl_btns = document.querySelectorAll("#btn_edit");

tbl_btns.forEach(function(elem) {
	elem.addEventListener("click", function(e) {
		e.preventDefault();
		var x = getSelected(e.srcElement);
		console.log(x);
	});
});

function getSelected(e){

	//first TD
	var id = e.parentNode.parentNode.cells[0].children[0].getAttribute('data-id');

	//second TD
	var forum_name = e.parentNode.parentNode.cells[1].children[0].text;

	//fourth TD
	var forum_private = e.parentNode.parentNode.cells[3].childElementCount;

	return { id, forum_name, forum_private };
}
```

* * *

Optimize more!

```js
Array.prototype.forEach.call(document.querySelectorAll('#btn_edit'), function(el) {

	el.addEventListener('click', function(e) {
		e.preventDefault();
		var x = getSelected(e.srcElement);
		console.log(x);
	})

})

function getSelected(e){

	var tr = e.parentNode.parentNode;

	var id = tr.cells[0].children[0].getAttribute('data-id');
	var forum_name = tr.cells[1].children[0].text;
	var forum_private = tr.cells[3].childElementCount;

	return { id, forum_name, forum_private };
}
```

greets to [https://plainjs.com/](https://plainjs.com/) and [joyrexus](https://gist.github.com/joyrexus/7307312)

origin - http://www.pipiscrew.com/?p=13786 selecting-multiple-elements-with-the-same-id-using-queryselectorall-and-use-the-returned-nodelist-object