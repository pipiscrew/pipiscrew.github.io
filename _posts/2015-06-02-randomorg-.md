---
title: random.org call
author: PipisCrew
date: 2015-06-02
categories: []
toc: true
---

```js
//test

			$(function() {

				//button click
				$('#btn').on('click', function(e) {

					if ($("#txt_how_many").val().length == 0 || 
					$("#txt_min").val().length == 0 ||
					$("#txt_max").val().length == 0)
					{alert( "Please fill textboxes!");
					return;
					}
					//window.open("http://www.random.org/integers/?num=" + $("#txt_how_many").val() + "&min=" + $("#txt_min").val() + "&max=" + $("#txt_max").val() + "&col=1&base=10&format=plain&rnd=new")

		 			$.ajax({
		                url: 'https://api.random.org/json-rpc/1/invoke',
		                dataType : 'json',
		                contentType: "application/json-rpc", 
		                type: 'POST',
		                data:  JSON.stringify({
		                    "jsonrpc": "2.0",
		                    "method": "generateSignedIntegers",
		                    "params": {
		                        "apiKey": "x-x-x-8b27-x", //get your http://api.random.org/api-keys/beta
		                        "n": $("#txt_how_many").val(),
		                        "min": $("#txt_min").val(),
		                        "max":  $("#txt_max").val(),
								"replacement" : false, //by default true - the resulting numbers may contain duplicate values
								"base" : 10
		                    },
		                    "id": 14215333
		                    })

		            })
		            .done(function (data, status, request)
		            {
		            	console.log(data);
		            	if (data.error)
		            	{
		            		alert(data.error.message);
		            	}

		            	if (data)
		            		if (data.result)
		            			if (data.result.random)
			            		{
			            			var nos = data.result.random.data;
			            			//console.log(nos);
			            			var outp = "";
			            			for(var no in nos)
			            			{
			            				outp += nos[no] + "  
";
			            				//console.log(nos[no]);
			            			}

			            			$("#myDIV").html(outp);
			            		}

		            })
		            .fail(function (request, status, error)
		            {
		                alert("Failed " + error);
		            });

			});

		});

		<div style="margin: 0 auto;width:500px">
			  <div class="form-group">
			    <label for="exampleInputEmail1">Generate Numbers : </label>
			    <input class="form-control" id="txt_how_many" placeholder="Numbers">
			  </div>

			  <div class="form-group">
			    <label>Minimum Number : </label>
			    <input class="form-control" id="txt_min" value="1" placeholder="Minimum Number">
			  </div>

			  <div class="form-group">
			    <label>Maximum Number : </label>
			    <input class="form-control" id="txt_max" placeholder="Maximum Number">
			  </div>

				<button id="btn">
					Generate
				</button>

<div id="myDIV" style="text-align: center"></div>  

		</div>

```

origin - http://www.pipiscrew.com/?p=3086 js-random-org-call