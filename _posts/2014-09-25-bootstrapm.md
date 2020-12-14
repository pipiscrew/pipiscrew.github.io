---
title: o[bootstrap+mysql+php] datetimepicker
author: PipisCrew
date: 2014-09-25
categories: []
toc: true
---

 **reference** 
[http://www.malot.fr/bootstrap-datetimepicker/](http://www.malot.fr/bootstrap-datetimepicker/)

<span style="color: #ff0000;">**[--READ_RECORD.html--]**</span>

****PHP+TSQL :**
//DATE_FORMAT(meeting_datetime,'%d-%m-%Y %H:%i') - 24h format

```js
<?php $row="null;" read="" specific="" record="" date_format(meeting_datetime,'%d-%m-%y="" %h:%i')="" -="" 24h="" if="" (isset($_get["id"]))="" {="" $find_sql="SELECT client_id, DATE_FORMAT(meeting_datetime,'%d-%m-%Y %H:%i') as meeting_datetime FROM clients where client_id = :id" ;="" $stmt="$db-"?>prepare($find_sql);
	$stmt->bindValue(':id', $_GET["id"]);

	$stmt->execute();
	$row = $stmt->fetchAll();
}
?>
```

****JS - jQuery Init Datetime Control :**

```js
    $('[name=meeting_datetime]').datetimepicker({
		weekStart: 1,
		todayBtn:  1,
		autoclose: 1,
		todayHighlight: 1,
		startView: 2,
		forceParse: 1
    });
```

****JS - Set Datetime Control :**

```js
    //set to JS variable the PHP variable as JSONarray!
    var jArray = ;
    $('[name=meeting_datetime]').val(jArray[0]["meeting_datetime"]);
```

****HTML**

```js
<!-- data-date-format=dd-mm-yyyy hh:ii - 24h format -->
<form id="leads_FORM" action="SAVE_RECORD.php" method="post">
<div class="col-xs-6 col-md-4"><label>Meeting Datetime :</label>

 <input class="form_datetime" type="text" name="meeting_datetime" readonly="readonly" data-date-format="dd-mm-yyyy hh:ii"></div>
 <button id="btn_leads_details_save" class="btn btn-primary" name="submit" type="submit">
 save
 </button></form>

    ```

    <span style="color: #ff0000;">**[--SAVE_RECORD.php--]**</span>

    ```js
    <?php $meeting_datetime="null;" if="" (!empty($_post['meeting_datetime']))="" {="" convert="" html="" control="" 24h="" date="" -="" to="" php="" 24h="" format="" date="" $dt="DateTime::createFromFormat('d-m-Y" h:i',="" $_post['meeting_datetime']);="" set="" to="" variable="" a="" string="" date="" formatted="" as="" mysql="" likes!="" $meeting_datetime="$dt-"?>format('Y-m-d H:i:s');
    }

        $sql = "INSERT INTO clients (meeting_datetime) VALUES (:meeting_datetime)";
        $stmt = $db->prepare($sql);
        $stmt->bindValue(':meeting_datetime' , $meeting_datetime); //$_POST['meeting_datetime']);
        $stmt->execute();
        $res = $stmt->rowCount();

    if($res == 1)
        //record saved
    else
        //error?
    ```

    where the datetime field is nullable :
    ```js
    CREATE TABLE clients (
      client_id int(11) NOT NULL AUTO_INCREMENT,
      meeting_datetime datetime DEFAULT NULL
      PRIMARY KEY (client_id)
    )
    ```

    ![](https://www.pipiscrew.com/wp-content/uploads/2014/09/snap036.png "snap036")

origin - http://www.pipiscrew.com/?p=1381 bootstrapmysqlphp-datetimepicker