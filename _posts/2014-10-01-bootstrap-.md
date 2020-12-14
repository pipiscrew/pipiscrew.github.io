---
title: bootstrap animated progress
author: PipisCrew
date: 2014-10-01
categories: []
toc: true
---

reference http://getbootstrap.com/

> no picture needed all included on bootstrap css

```js
		<style>
			/*progress*/
			.modal-backdrop { opacity: 0.7;	filter: alpha(opacity=70);	background: #fff; z-index: 2;}
			div.loading { position: fixed; margin: auto; top: 0; right: 0; bottom: 0; left: 0; width: 200px; height: 30px; z-index: 3; }
		</style>
```

```js
//**the div using the styling^
			var loading = $('<div class="modal-backdrop"></div><div class="progress progress-striped active loading"><div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">');

				//EXAMPLE - AJAX CALL (edit button - read record by server)
				function query_CLIENT_modal(rec_id){
					//**the USE
					loading.appendTo(document.body);

				    $.ajax(
				    {
				        url : "x.php",
				        type: "POST",
				        data : { client_id : rec_id },
				        success:function(data, textStatus, jqXHR)
				        {
						//**the USE
						loading.remove();

				        	if (data!='null')
							{
								$('#modalCLIENT_APPOINTMENTS').modal('toggle');
							}
							else
								alert("ERROR - Cant read the record.");
				        },
				        error: function(jqXHR, textStatus, errorThrown)
				        {
						//**the USE
						loading.remove();

				            alert("ERROR");
				        }
				    });
				}
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/10/snap054.png "snap054")</div></div>

origin - http://www.pipiscrew.com/?p=1416 bootstrap-animated-progress