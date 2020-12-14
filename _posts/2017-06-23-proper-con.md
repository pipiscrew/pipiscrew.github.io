---
title: Proper convert UTC to Browser time
author: PipisCrew
date: 2017-06-23
categories: [js,php,sql]
toc: true
---

```js
//src - //https://stackoverflow.com/a/13622393/1320686

////try 01
//when is Daylight saving time (DST) *NOT* applied
var dateStr =  '11/30/2016 3:05:24 AM UTC';
var date = new Date(dateStr);
console.log("*1*", date.toString()); 

////try 02 *universal*
//when is Daylight saving time (DST) applied
var dateStr2 =  '11/30/2016 3:05:24 AM';
var date2 = new Date(dateStr2);
var offset = new Date().getTimezoneOffset(); //get the diff from UTC
//for all zones that are GMT+, the result is a negative number
//for GMT-, the result is a positive number
//example Im on GMT+2 (DST), the result is -120

date2.setMinutes(date2.getMinutes() - offset);

console.log("*2*", date2.toString()); 

--

output :
*1* Wed Nov 30 2016 04:05:24 GMT+0100 (Central Europe Standard Time)
*2* Wed Nov 30 2016 05:05:24 GMT+0100 (Central Europe Standard Time)

--
////////////////////////////////////////////////////////////////////////
//in PHP, we passing the JS 'diff from UTC' and using the same technic

$dateStr2 =  '11/30/2016 3:05:24 AM';

$a='-120'; //come from AJAX? 

if (is_int($a)) //http://php.net/manual/en/function.is-int.php
   echo date('Y-m-d H:i:s', strtotime($dateStr2. " -$a minutes"));

--

output :
2016-11-30 05:05:24

//ps - *date_default_timezone_set* doesnt take place^

--

////////////////////////////////////////////////////////////////////////
//in MySQL we passing the JS 'diff from UTC' and using the same technic
select date_rec + INTERVAL --120 MINUTE from answers
where date_rec = '2016/11/30 3:05:24'
//even is 
//date_rec = '2016/11/30 3:05:24 AM' 0R date_rec = '2016/11/30 3:05:24 PM'
//returns the record

--

output :
2016-11-30 05:05:24
```

JS and PHP Snippet

```js
//src by Westy92 - http://www.westy92.com/?p=54

    $(document).ready(function() {
        if("<?php echo $timezone; ?>".length==0){
            var visitortime = new Date();
            var visitortimezone = "GMT " + -visitortime.getTimezoneOffset()/60;
            $.ajax({
                type: "GET",
                url: "http://domain.com/timezone.php",
                data: 'time='+ visitortimezone,
                success: function(){
                    location.reload();
                }
            });
        }
    });

<?php
    session_start();
    $_SESSION['time'] = $_GET['time'];
?>
```

Put it all together!

```js
//login.php
//this form POST to itself
<?php
    session_start();
    date_default_timezone_set("UTC");

    require_once('general.php');

    $db = new dbase();
    $db->connect_mysql();

    $message = null;

    ////////////////////////////LOGIN USER

    if ($_SERVER['REQUEST_METHOD'] === 'POST') {

        $message=null;

        if (!isset($_POST["u"]) && !isset($_POST["p"]) && !isset($_POST["t"]))
        {
            $message = "Please fill username and password.";
        }

        if (empty($_POST['u']) || empty($_POST['p']) || empty($_POST['t'])) {
            $message = "Please fill username and password.";
        }
        else {

            $user_timezone = intval($_POST["t"]);

            $pwd_md5 = md5($_POST["p"]); //convert plain text to md5

            //get the dbase password for this mail
            $r = $db->getRow("select user_id,user_level,user_name from users where user_name=? and user_password=?",array($_POST['u'], $pwd_md5));

            //^if record exists
            if ($r){
                    $_SESSION['id'] = $r["user_id"];
                    $_SESSION['level'] = (int) $r["user_level"];
                    $_SESSION['name'] = $r["user_name"];
                    $_SESSION['login_expiration'] = date("Y-m-d");
                    $_SESSION['timezone'] = (string) $user_timezone;

                    if ($_SESSION['level']==1)
                        header("Location: user.php");
                    else 
                        header("Location: index.php");

            } else {
                $message = "Couldnt find a user for the login combination provided.";
            }
        }

    }

?>

		<div class="container">
            <?php if ($message!=null) { ?>
                <div class="alert alert-danger"><?php echo $message;?> </div>
            <?php }; ?>

            <button class="btn btn-sm btn-success" onclick="location.href = 'register.php'" style="float:right">Register new user</button>

			<div class="form-signin">
				<form class="form-signin" method="post">

## Login

					<input name="u" type="text" class="form-control" placeholder="username" autofocus required>
					<input name="p" type="password" class="form-control" placeholder="password" required>
                    <input name="t" id="t" hidden>

					<button class="btn btn-lg btn-primary btn-block" type="submit" name="submit" id="login">
						login
					</button>
				</form>
			</div>
		</div>

            //set user timezone to input
            document.getElementById('t').value = new Date().getTimezoneOffset();

<?php require_once('footer.php'); ?>

```

```js
//index.php
<?php
	session_start();
	date_default_timezone_set("UTC");

	if (!isset($_SESSION["id"])) {
        session_destroy(); //destroy the session
		header("Location: login.php");
		exit ;
	}
	else {

		if ($_SESSION["login_expiration"] != date("Y-m-d"))
		{	
            session_destroy(); //destroy the session
            header("Location: login.php");
			exit ;
		}

        if (!isset($_SESSION['timezone']))
		{	
            session_destroy(); //destroy the session
            header("Location: login.php");
			exit ;
		}  

        if ($_SESSION['level'] == 1)
		{	
            session_destroy(); //destroy the session
            header("Location: login.php?q=Invalid User Level for Admin Panel");
			exit ;
		} 

	}

$find_sql = "SELECT plaintext_id, categories.category_name as category, languages.language_name as language_id, plaintext_title
, date_rec + INTERVAL -{$_SESSION['timezone']} MINUTE as date_rec FROM `plaintexts`
 LEFT JOIN categories ON categories.category_id = plaintexts.category_id
 LEFT JOIN languages ON languages.language_id = plaintexts.language_id";

 //OR

select question_id, categories.category_name as category_name,  questions.subcategory_id as subcategory_id, subcategories.subcategory_name as subcategory_name, languages.language_name as language_id, title, question, misc1, misc2, misc3, misc4, (date_rec + INTERVAL -:browsertime MINUTE) as date_rec from questions 
 LEFT JOIN categories ON categories.category_id = questions.category_id
 LEFT JOIN subcategories ON subcategories.subcategory_id = questions.subcategory_id
 LEFT JOIN languages ON languages.language_id = questions.language_id
 limit :offset,:limit

//////////////////////////////////////BIND PARAMS
$stmt->bindValue(':offset' , intval($offset), PDO::PARAM_INT);
$stmt->bindValue(':limit' , intval($limit), PDO::PARAM_INT);
$stmt->bindValue(':browsertime' , intval($_SESSION['timezone']), PDO::PARAM_INT);

//////////////////////////////////////FETCH ROWS
$stmt->execute();

$rows = $stmt->fetchAll();

 //OR

$find_sql = "SELECT plaintext_id, language_id, category_id, plaintext_title, the_text
, (date_rec + INTERVAL -? MINUTE) as date_rec FROM `plaintexts` where plaintext_id = ?";

$row = $db->getSet($find_sql, array($_SESSION['timezone'], $_GET["id"]));
?>
```

origin - http://www.pipiscrew.com/?p=8441 proper-convert-utc-to-browser-time