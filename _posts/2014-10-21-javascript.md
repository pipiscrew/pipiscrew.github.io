---
title: o[javascript] anchor with href+reload page
author: PipisCrew
date: 2014-10-21
categories: []
toc: true
---

using a PHP script with fread method, to download a private file (CHMOD=600), I realize that cant redirect the user, using **header(..)** function, after download.. whats next? javascript!!

```js
	//dynamic handler for grid buttons
	$(document).on("click", "#invoice_download", function(e) {
		location.reload(true);					
	});

	 var jArray_contracts =   <?php echo="" json_encode($contracts);=""?>;

	 var combo_contracts_rows = "";
	 for (var i = 0; i < jarray_contracts.length;="" i++)="" {="" combo_contracts_rows="" +="<td><a id='invoice_download' target='_blank' href='download.php?id=" +="" jarray_contracts[i]["offer_id"]="" +="" "'="" class='btn btn-danger btn-xs'>Download";
	 }

	 $("#contracts_rows").html(combo_contracts_rows);

	<table id="contracts_tbl">					
		<tbody id="contracts_rows"></tbody>
	</table>
```

for each table row, I set 
```js
 [Download](download.php?id=)
```

plus at javascript a jQ dynamic anchor click event handler, **without use** the famous 
```js
e.preventDefault();
```
to prevent the href redirection.

when click the anchor, the result is : 
-a new tab popup and call the download function (external PHP file)
-at the same time reload the page (has the grid, contains the anchor) to update the record status

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap097.png "snap097")

origin - http://www.pipiscrew.com/?p=1575 javascript-anchor-with-hrefreload-page