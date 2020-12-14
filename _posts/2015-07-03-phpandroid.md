---
title: o[php+android] secure connection with session variable
author: PipisCrew
date: 2015-07-03
categories: []
toc: true
---

references :
[http://www.lightrains.com/blog/simple-tip-session-handling-android](http://www.lightrains.com/blog/simple-tip-session-handling-android)
[http://www.programering.com/a/MTMwATNwATg.html](http://www.programering.com/a/MTMwATNwATg.html) *or* [http://www.cnblogs.com/kross/p/3615695.html](http://www.cnblogs.com/kross/p/3615695.html)
[http://www.yoyong.com/archives/178](http://www.yoyong.com/archives/178) *or* [link2](http://www.apkbus.com/android-5908-1.html) *or* [link3](http://www.apkway.com/thread-6670-1-1.html)
[http://www.capri-soft.de/blog/?p=652](http://www.capri-soft.de/blog/?p=652)
[http://stackoverflow.com/a/5948059/1320686](http://stackoverflow.com/a/5948059/1320686)
[http://stackoverflow.com/questions/3587254/how-do-i-manage-cookies-with-httpclient-in-android-and-or-java](http://stackoverflow.com/questions/3587254/how-do-i-manage-cookies-with-httpclient-in-android-and-or-java)

the prototypes referenced are by **cnblogs.com**

<font size="6">Prototype 1 - using DefaultHttpClient</font>

<span style="color: #ff0000;">**//JAVA - Activity button**</span>

```js
	public void btnAdd2_Click(View view)
	{
		StrictMode.ThreadPolicy policy = new StrictMode.ThreadPolicy.Builder().permitAll().build();
		StrictMode.setThreadPolicy(policy);

		try {
			NetClient n = new NetClient();

			String k = n.login("http://x.com/testAREA/securetrans/login.php");
			Log.w("login result", k);

			String l = n.request("http://x.com/testAREA/securetrans/content.php");
			Log.w("ask if logged in", l);

		} catch (ClientProtocolException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
```<span style="color: #ff0000;">**//JAVA Class**</span>

```js
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;

import org.apache.http.HttpResponse;
import org.apache.http.NameValuePair;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.HttpClient;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.message.BasicNameValuePair;

public class NetClient {

    private HttpClient client = null;

    public NetClient() {
        client = new DefaultHttpClient();
    }

    public String request(String url) throws ClientProtocolException, IOException {
        HttpPost post = new HttpPost(url);
        HttpResponse res = client.execute(post);

        BufferedReader br = new BufferedReader(new InputStreamReader(res.getEntity().getContent()));
        String data = "";
        String line = "";
        while ((line = br.readLine()) != null) {
             data = data + line;
        }
        return data;
    }

    public String login(String url) throws ClientProtocolException, IOException {
        HttpPost post = new HttpPost(url);

        ArrayList pa = new ArrayList();
        pa.add( new BasicNameValuePair( "username", "admin"));
        pa.add( new BasicNameValuePair( "password", "admin"));
        post.setEntity( new UrlEncodedFormEntity(pa, "UTF-8"));

        HttpResponse res = client.execute(post);

        BufferedReader br = new BufferedReader(new InputStreamReader(res.getEntity().getContent()));
        String data = "";
        String line = "";
        while ((line = br.readLine()) != null) {
             data = data + line;
        }
        return data;
    }
}
```

<span style="color: #ff0000;">**//A login form post itself when browse normally (from browser)**</span>
<span style="color: #ff0000;"> **//login.php**</span>

```js
<?php session_start();="" if(isset($_post['username']))="" {="" $username="$_POST['username'];" $password="$_POST['password'];" if($username="=" 'admin'="" &&="" $password="=" 'admin')="" {="" $_session['username']="$username;" echo="" "admin="" setted";="" exit;="" }="" else="" {="" echo="" "-1";="" }="" }=""?>

		<form action="" method="post">
			<input type="text" name="username">
			<input type="password" name="password">
			<input type="submit" name="submit" value="submit">
		</form>

```

<span style="color: #ff0000;">**//the result page**</span>
<span style="color: #ff0000;"> **//content.php**</span>

```js
<?php session_start();="" if(isset($_session['username']))="" {="" echo="" "login="" ok";="" }="" else="" {="" echo="" "not="" login";="" }=""?>
```

By the result, we understand that the session variable **$_SESSION['username']** retained from **login.php** to **content.php** :
![](https://www.pipiscrew.com/wp-content/uploads/2014/11/snap222.png "snap222")

thats nice :), time to develop!

* * *

<center><font size="6">Prototype1 - MixUP!</font></center>

> proper way - sample android java project + PHP files
> -create an application class
> -create custom http class, using application context DefaultHttpClient

<center>[![](https://www.pipiscrew.com/wp-content/uploads/2014/11/download_button.png "download")](https://pipiscrew.com/Downloads/doc_securetrans.zip)</center>

* * *

<center><font size="6">Prototype 2 - Using cookie method</font></center>

using the same code as Prototype1, we replace NetClient class with NetHelper and the referenced calls. We make it work without the need of class shared **DefaultHttpClient**. 

> Yahel writes :Your Php script uses a session token to identify the visitor when you browse the site via a browser. Ususally its stored in a PHPSESSID variable.
> If you want your Android application to stay authenticated on the server side you need to fetch that id after the first connection and then send it in the headers of all your subsequent requests.

line **54-55** = fetch PHPSESSID and store it for later calls 
aka **login()** function, run only once, then on all the other calls use the **request()**. Check line **22** which using the **sessionId**.

```js
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class NetHelper {

    /**
     * SESSIONID
     * */
    private String sessionId = "";

    /**
     * Send a request, the content in a string
     * @param The address of the URL request
     * @return The content returned
     * */
    public String request(String url) throws IOException {
        URL uUrl = new URL(url);
        HttpURLConnection huc = (HttpURLConnection) uUrl.openConnection();
        huc.addRequestProperty("Cookie", sessionId);    //Why is "Cookie", open Chrome press F12 and check!
        huc.connect();
        BufferedReader br = new BufferedReader(new InputStreamReader(huc.getInputStream()));
        String data = "";
        String line = "";
        while ((line = br.readLine()) != null) {
             data = data + line;
        }
        return data;
    }

    /**
     * Sends the login request, and the SESSIONID store
     * @param The URL login request
     * @return The content returned
     * */
    public String login(String url) throws IOException {
        URL uUrl = new URL(url);
        HttpURLConnection huc = (HttpURLConnection) uUrl.openConnection();

        //Set the request
        huc.setRequestMethod("POST");

        //Set the post parameters
        StringBuffer params = new StringBuffer();
        params.append("username=").append("admin").append("&").append("password=").append("admin");
        byte[] bytes = params.toString().getBytes();
        huc.getOutputStream().write(bytes);

        huc.connect();

        //Take out, from the headers the ID segmentation, open Chrome press F12 and check!
        String[] aaa = huc.getHeaderField("Set-Cookie").split(";");
        sessionId = aaa[0];

        BufferedReader br = new BufferedReader(new InputStreamReader(huc.getInputStream()));
        String data = "";
        String line = "";
        while ((line = br.readLine()) != null) {
             data = data + line;
        }
        return data;
    }
}
```

* * *

<center><font size="6">Prototype2 - MixUP!</font></center>

> proper way - sample android java project + PHP files
> -create an application class
> -create custom http class, using application context php_session_id

<center>[![](https://www.pipiscrew.com/wp-content/uploads/2014/11/download_button.png "download")](https://pipiscrew.com/Downloads/doc_securetrans.zip)</center>

* * *

in CSharp 
```js
        private void button1_Click(object sender, EventArgs e)
        {
            //http://stackoverflow.com/a/931030

            // NOTE: This is the URL the form POSTs to, not the URL of the form (you can find this in the "action" attribute of the HTML's form tag
            string formUrl = "http://www.x.com/api/login.php";
            string formParams = string.Format("email={0}&pass={1}&submit={2}", "c@x.com", "543654364", "test");
            string cookieHeader;
            WebRequest req = WebRequest.Create(formUrl);
            req.ContentType = "application/x-www-form-urlencoded";
            req.Method = "POST";
            byte[] bytes = Encoding.ASCII.GetBytes(formParams);
            req.ContentLength = bytes.Length;
            using (Stream os = req.GetRequestStream())
            {
                os.Write(bytes, 0, bytes.Length);
            }
            WebResponse resp = req.GetResponse();
            cookieHeader = resp.Headers["Set-cookie"];
            Console.WriteLine(cookieHeader); //read PHPSESSID

            StreamReader sr = new StreamReader(resp.GetResponseStream());
            Console.WriteLine(sr.ReadToEnd()); //read RESPONSE
        }
```

GET request to a page that you need to be logged in.
```js
string pageSource;
string getUrl = "http://www.x.com/where.session.validated.at.php.side.php";
WebRequest getRequest = WebRequest.Create(getUrl);
getRequest.Method = "POST"; //we can make a POST request!
//must be as example #PHPSESSID=assssbj6tb30ljttm4q4olpjn0#, warning no spaces!
getRequest.Headers["Cookie"] = "PHPSESSID=" + php_sessid;
// working also - getRequest.Headers.Add("Cookie",  "PHPSESSID=" + php_sessid);
WebResponse getResponse = getRequest.GetResponse();
using (StreamReader sr = new StreamReader(getResponse.GetResponseStream()))
{
    pageSource = sr.ReadToEnd();
}
```

* * *

## PERSISTENT SESSIONS WITH PHP

[http://www.paulsrichards.com/2008/07/29/persistent-sessions-with-php/](http://www.paulsrichards.com/2008/07/29/persistent-sessions-with-php/)

source - [http://www.amazon.co.uk/Essential-PHP-Security-Chris-Shiflett/dp/059600656X/](http://www.amazon.co.uk/Essential-PHP-Security-Chris-Shiflett/dp/059600656X/)

```js
//Outline Example
//Ok, you’ve authenticated your users username and password and they’ve indicated that they wish to remain logged in for one week.

// This examples assumes you have already connected to a MySQL database
$salt = "pAulR2";
/*
  You must create a identifier for every user and store it in the database prior implementing this.
  $identifier = md5( $salt . md5($username . $salt ) );
*/
// retrieve the $identifier from the database, I'm going to assume its in a variable called
// $user['identifier']
$identifier = $user['identifier'];

// create a random key
$key = md5(uniqid(rand(), true);
// calculate the time in 7 days ahead for expiry date
$timeout = time() + 60 * 60 * 24 * 7;

// Set the cookie with information
setcookie('authentication', "$identifier:$key", $timeout);
// now update the database with the new information
$result = mysql_query("UPDATE user SET key = '$key', timeout = '$timeout'
WHERE username = '$username'");
if (!$result) {
    die('Invalid query: ' . mysql_error());
}
```

```js
//Right that takes care of setting the cookie but know we must authorise it when its been detected when the user comes back to the site. On the users first visit you need to implement code like the following:

$salt = "pAulR2";

if (isset($_COOKIE['authentication'])) {
    // cookie is set, lets see if its vailed and log someone in
    $clean = array();
    $mysql = array();

    $now = time();

    list($identifier, $token) = explode(':', $_COOKIE['authentication']);
    if (ctype_alnum($identifier) && ctype_alnum($token)) {
	$clean['identifier'] = $identifier;
	$clean['key'] = $key;

	$mysql['identifier'] = mysql_real_escape_string($clean['identifier']);

	$result = mysql_query("SELECT * FROM user
                                       WHERE identifier = '{$mysql['identifier']}'");
	if (mysql_num_rows($result)) {
		$record = mysql_fetch_assoc($result);
		if ($clean['key'] != $record['key']) {
			// fail because the key doesn't match
		}elseif ($now > $record['timeout']){
			// fail because the cookie has expired
		}elseif ($clean['identifier'] != md5($salt.md5($record['userID'].$salt))){
			// fail because the identifiers does not match
		}else{
			/*
                          Success everything matches, now you can process
                          your login functions. The key must be re generated
                          for the next login. But don't increase the timeout to
                          ensure that the user must login in once the time
                          period has passed.
                       */
	        }
	}
	}else {
			/* failed because the information is not in the
                            correct format in the cookie */
        }
}
```

origin - http://www.pipiscrew.com/?p=1754 phpandroid-secure-connection-with-session-variable