---
title: localStorage
author: PipisCrew
date: 2015-08-23
categories: [Uncategorized]
toc: true
---

HTML5 Client Side Storage (Local Storage and Session Storage) - [http://www.dotnetcurry.com/html5/1001/html5-client-side-local-session-storage](http://www.dotnetcurry.com/html5/1001/html5-client-side-local-session-storage)

```js

	$(function() {
        //clear
        localStorage.clear();   

        //construct array + add items
        var d= [];
        d[0] =  {'name' :'costas','age':23};
        d[1] =  {'name' :'test','age':18};

        //save values to localDB via JSON stringify
        localStorage["costas_dbase"] = JSON.stringify(d);

        //read items from localDB via JSON parse
        var storedNames = JSON.parse(localStorage["costas_dbase"]);

        //print out the array size
        console.log("total recs - " + storedNames.length);

        //print out the object itself
        console.log(storedNames.length);

        //clear localDB
        //localStorage.clear();   
	});

```

## Complete Example

```js
//grets to my friend Philip!

<style type="text/css">
    div {
        padding: 5px;
        float: left 3px;
    }
   table{
        width: 100%;
        padding: 2px;
    }
   th {
        background-color: #940bf8;
        color: #e8e805;
       height: 30px;
       text-align: center;
       vertical-align: middle;
   }

/*
    body{
        background-color: #d3d2d2;
    }
*/
 /*
    label {
        background-color: cyan;
        color: crimson
    }
*/
</style>

			$(function() {

                fill_grid("onRender");

                $("#done").click(function(){ //on click save

                    //read local db
                    var stats = localStorage["namco_dbase"];
                    var dx= [];
                    var i = 0;
                    console.log(stats)
                    if (stats) //if exists
                    {
                        //JSON DECODE
                        var storedNames = JSON.parse(localStorage["namco_dbase"]);
                        var arr_length = storedNames.length;

                        //for each in array
                        storedNames.forEach(function(entry) {
                           dx[i] = entry;
                            i+=1;

                        }); 
                    }

                    if ($("#fname").val().trim().length==0 || $("#lname").val().trim().length==0 || $("#locate").val().trim().length==0)
                    {
                        alert("Please fill the required fields1 (*) ");
                        return;
                    }

                    if  ($("#dance").val()=="999" || $("#type").val() =="999"|| $("#focus").val() =="999"|| $("#exp").val() =="999"|| $("#sex").val() =="999"|| $("#pos").val() =="999"|| $("#occasion").val()=="999")
                    {
                        alert("Please fill the required fields2 (*) ");
                        return;
                    }

                    dx[i] ={'first' :$("#fname").val(),'last' :$("#lname").val(),'location' :$("#locate").val(),'dance' :$("#dance").val(),'type' :$("#type").val(),'focus' :$("#focus").val(),'experience' :$("#exp").val(),'sex' :$("#sex").val(),'position' :$("#pos").val(),'occasion' :$("#occasion").val()};

                    //save values to localDB via JSON stringify 
                    localStorage["namco_dbase"] = JSON.stringify(dx);

                    if(confirm("Do you like to update the grid dynamically?"))
                    {
                        fill_grid("onSave");
                        init_ctls("onSave");
                    }
                    else 
                        //when stored, reload
                        location.reload();                        

                })

            $("#new").click(function() //on click new
                            {

                        init_ctls("onNew");

            })

            }) //jQ ends

            function init_ctls()
            {
                $("#fname").val('');
                $("#lname").val('');
                $("#locate").val('');
                $("#exp").val(999);
            }

            function fill_grid(caller)
            {
                console.log(caller);

                //onpage render - read the dbase
                var stats = localStorage["namco_dbase"];

                if (stats) //if exists
                { 
                    var records = JSON.parse(stats);
                    $("#records_info").html("Total Records : " + records.length);

                    var tbl="";
                    //for each in array
                    records.forEach(function(entry) {
                       tbl+="<tr>"
                       tbl+="<td><a href='#' onClick=\"get_item_details('"+ entry["first"]+"','"+ entry["last"]+"','"+ entry["location"]+"','"+entry["dance"]+"','"+entry["position"]+"')\">" + entry["first"] + "</a></td><td>"  + entry["last"] + "</<td><td>"  + entry["location"] + "</td><td>"  + entry["dance"] + "</td><td>"  + entry["position"] + "</td>"; 
                       tbl+="</tr>"
                    }); 
                    console.log(tbl);
                    $("#tbl_rows").html(tbl);
                }
                else 
                    $("#records_info").html("Total Records : 0");
            }

            function get_item_details(fname,lname,loc,dance,pos)
            {
                    //read local db
                    var stats = localStorage["namco_dbase"];
                    var dx= [];
                    var i = 0;
                    console.log(stats)
                    if (stats) //if exists
                    {
                        //JSON DECODE
                        var storedNames = JSON.parse(localStorage["namco_dbase"]);

                        //for each in array
                        storedNames.forEach(function(entry) {
                          if (entry["first"] == fname && entry["last"] == lname)
                          {
                              $("#fname").val(entry["first"]);
                              $("#lname").val(entry["last"]);
                              $("#locate").val(entry["location"]);
                              $("#exp").val(entry["experience"]);

                              return false; //exit by forEach loop
                          }

                        }); 
                    }
            }

        <center>

# Ballroom Dance

</center>

        <div id="records_info" style="color:red;"> </div>

<div class="row">
    <div class="col-md-3">
          <div class="form-group">
            <label>* FName</label>
            <input class="form-control" type="text" id="fname" placeholder="First Name">
          </div>
    </div>

    <div class="col-md-3">
          <div class="form-group">
            <label>* LName</label>
            <input class="form-control" type="text" id="lname" placeholder="Last Name">
          </div>
    </div>

    <div class="col-md-3">
          <div class="form-group">
            <label>* Location</label>
            <input class="form-control" type="text" id="locate" placeholder="City, Country">
          </div>
    </div>

    <div class="col-md-3">
          <div class="form-group">
            <label>Previous Experience</label>
                <select class="form-control" id="exp">
                    <option value="999">
                    <option>Yes
                    <option>No
                </select>
          </div>
    </div>

</div>

    <center>
        <button class="btn-success" id="done" name="done">SAVE</button>
        <button class="btn-danger" id="new" name="new">NEW</button>
    </center>

        <table id="tbl" border="1px grey;">
            <th><span style="margin-right:5px;" class="glyphicon glyphicon-user" aria-hidden="true"></span>FName<span style="margin-left:5px;" class="glyphicon glyphicon-user" aria-hidden="true"></span></th>
            <th><span style="margin-right:5px;" class="glyphicon glyphicon-tags" aria-hidden="true"></span>LName<span style="margin-left:5px;" class="glyphicon glyphicon-tags" aria-hidden="true"></span></th>
            <th><span style="margin-right:5px;" class="glyphicon glyphicon-home" aria-hidden="true"></span>Location<span style="margin-left:5px;" class="glyphicon glyphicon-home" aria-hidden="true"></span></th>
            <th><span style="margin-right:5px;" class="glyphicon glyphicon-music" aria-hidden="true"></span>Dance<span style="margin-left:5px;" class="glyphicon glyphicon-music" aria-hidden="true"></span></th>
            <th><span style="margin-right:5px;" class="glyphicon glyphicon-hand-right" aria-hidden="true"></span>Position<span style="margin-left:5px;" class="glyphicon glyphicon-hand-left" aria-hidden="true"></span></th>

            <tbody id="tbl_rows">
            </tbody>
        </table>

```

origin - http://www.pipiscrew.com/?p=3088 js-localstorage