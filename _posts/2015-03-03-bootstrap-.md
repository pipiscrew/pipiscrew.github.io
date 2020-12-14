---
title: bootstrap-chooser.js
author: PipisCrew
date: 2015-03-03
categories: []
toc: true
---

**references**
http://learn.jquery.com/plugins/basic-plugin-creation/
http://stackoverflow.com/a/16504147 | http://jsfiddle.net/Meligy/s2wN4/
http://www.sitepoint.com/how-to-develop-a-jquery-plugin/
http://www.smashingmagazine.com/2011/10/11/essential-jquery-plugin-patterns/

copy&paste to **bootstrap-chooser.js**
```js
(function( $ ) {

    $.fn.getSelected = function() {
			var arr = new Array();

			this.children('a').filter(function(){
			    return $(this).attr('data-name')!=null && $(this).hasClass('list-group-item active');
			}).each(function(){
			    arr.push($(this).attr('data-name'));
			});

			return arr;
    };

    $.fn.setSelected = function(jsonArray, idColName){
			for (var i = 0; i < jsonarray.length;="" i++)="" this.children('a').each(="" function(index,="" element){="" if="" ($(this).attr('data-name')="=jsonArray[i][idColName])" {="" $(this).addclass('list-group-item="" active');="" return="" false;="" exit="" for="" each="" }="" });="" }="" $.fn.filllist="function(jsonArray," header,="" idcolname,descrcolname)="" {="" var="" cats="<a class='list-group-item active'> " +="" header="" +="" "="" :="">";

				for (var i = 0; i < jsonarray.length;="" i++)="" cats="" +="<a href='#' class='list-group-item' data-name='" +="" jsonarray[i][idcolname]="" +="" "'="">" + jsonArray[i][DescrColName] + "";

				//set result-rows to element
				this.html(cats);	
    };

    $.fn.clearList = function() {
			this.children('a').filter(function(){
		       return $(this).attr('data-name')==null;
			}).siblings().removeClass('list-group-item active').addClass('list-group-item');
    };

}( jQuery ));

$.fn.chooser = function() {
        $(this).on('click', 'a', function(event) {
						event.preventDefault();

						if (!$(this).attr('data-name'))
							return;

						if ($(this).hasClass('list-group-item active')) {
							$(this).removeClass('list-group-item active');
							$(this).addClass('list-group-item');
						} else {
							$(this).addClass('list-group-item active');
						}
					});

}
```

**sample html**
```js
<?php $rows_users="null;" read="" users="" if="" (isset($_get["id"]))="" {="" $find_sql="select * from users" ;="" $stmt="$db-"?>prepare($find_sql);
	$stmt->execute();
	$rows_USERS = $stmt->fetchAll();
}
///////////////////READ USERS
?>

    $(function() {
        //**attach the event
        $('#client_s_users').chooser();

        //**fill list by PHP/jSON Array
        var jArray_USERS = <? php echo json_encode($rows_USERS); ?> ;

        if (jArray_USERS)
            $("#client_s_users").fillList((jArray_USERS), "Participants", "user_id", "fullname");

        // MODAL FUNCTIONALITIES [START]
        //when modal closed, hide the warning messages + reset
        $('#modalCLIENT_S').on('hidden.bs.modal', function() {
            //when close - clear elements
            $('#formCLIENT_S').trigger("reset");

            //**reset users list
            $("#client_s_users").clearList();

            //clear validator error on form
            validatorCLIENT_S.resetForm();
        });

		//edit button - read record 
		function query_CLIENT_S_modal(rec_id){
			$.ajax(
			{
				url : "x_fetch.php",
				type: "POST",
				data : { x_id : rec_id },
				success:function(dataO, textStatus, jqXHR)
				{
					if (dataO!='null')
					{
						var data = dataO.appointment; //the record [ONE]
						var dataP = dataO.participants; // the details-record [MANY] (aka appear on chooser)

						//** USE of - select the values from DBASE^
						$("#client_s_users").setSelected(dataP,"user_id")

						$('#modalCLIENT_S').modal('toggle');
					}
					else
						alert("ERROR - Cant read the record.");
				},
				error: function(jqXHR, textStatus, errorThrown)
				{
					alert("ERROR");
				}
			});
		}

		//save form
		$('#form_APPOINTMENTS').submit(function(e)
			{
				e.preventDefault();

				////////////////////////// validation
				var form = $(this);
				form.validate();

				if (!form.valid())
				return;
				////////////////////////// validation

				//get #selected ids#
				var get_selected_participants = $("#client_appointments_users").getSelected();

				if (get_selected_participants.length==0)
				{
					alert("Please choose participants!");
					return;
				}

				var postData = $(this).serializeArray();
				var formURL = $(this).attr("action");

				//merge to serialization - stringify #selected ids#
				postData.push({name: "participants", value : JSON.stringify(get_selected_participants)});

				$.ajax(
					{
						url : formURL,
						type: "POST",
						data : postData,
						success:function(data, textStatus, jqXHR)
						{
							if (data=="00000")
								//refresh
								loadAPPOINTMENTSrecs();
							else
								alert("ERROR");
						},
						error: function(jqXHR, textStatus, errorThrown)
						{
							alert("ERROR - connection error");
						}
					});
			});
    }); //jQuery end

    <div id="client_s_users" class="list-group centre"></div>

```

```js
				//x_fetch.php ends as :
				$json = array('appointment'=> $r,'participants' => $x);
				echo json_encode($json);

				//x_save.php as :
				$arr = json_decode($_POST['participants'],true);

				$participants ="0";
				foreach ($arr as $userID) {
					$participants.= ",{$userID}";
				}

				//use it to find fullname
				$partSET = getSet($db,"select fullname from users where user_id in ({$participants})",null);
```

![](https://www.pipiscrew.com/wp-content/uploads/2014/09/snap045.png "snap045")

* * *

**Bootstrap.listgroup**
[http://rickardn.github.io/listgroup.js/](http://rickardn.github.io/listgroup.js/)

origin - http://www.pipiscrew.com/?p=1408 bootstrap-chooser-js