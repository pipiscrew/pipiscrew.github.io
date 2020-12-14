---
title: HttpPost minimal
author: PipisCrew
date: 2014-12-16
categories: []
toc: true
---

```js
        String URL = "http://x.com/sign_up.php";

		ArrayList<NameValuePair> nameValuePairs = new ArrayList<NameValuePair>();

		nameValuePairs.add(new BasicNameValuePair("email",email));
		nameValuePairs.add(new BasicNameValuePair("password", pass));

        HttpClient httpClient = new DefaultHttpClient();

        HttpPost post =  new HttpPost(URL); 
        post.setEntity(new UrlEncodedFormEntity(nameValuePairs));

        try {
    		HttpResponse response = httpClient.execute(post);

    		String responseString = EntityUtils.toString(response.getEntity());
            Log.w("test", responseString);
        } catch (IOException e) {
            e.printStackTrace();
        }
```

**optimized for JSON read**
```js
//get_records.php
$rows = getSet($db,"select * from mytable where OWNER_GUID=?",array($_POST['guid']));

if ($rows!=null)
	echo json_encode($rows);
```

```js
	public List<Automotos> getAutomotos(String auth) throws Exception {
        String URL = "http://x.com/get_records.php";

		ArrayList<NameValuePair> nameValuePairs = new ArrayList<NameValuePair>();

		nameValuePairs.add(new BasicNameValuePair("guid",auth));
		nameValuePairs.add(new BasicNameValuePair("tbl","automotos"));

        HttpClient httpClient = new DefaultHttpClient();

        HttpPost post =  new HttpPost(URL); 
        post.setEntity(new UrlEncodedFormEntity(nameValuePairs));

        List<Automotos> servList = new ArrayList<Automotos>();

        try {
    		HttpResponse response = httpClient.execute(post);

    		String responseString = EntityUtils.toString(response.getEntity());

    		JSONTokener tokener = new JSONTokener(responseString);
    		JSONArray jArray = new JSONArray(tokener);

    		for(int i=0; i<jArray.length(); i++){
    			JSONObject json_data = jArray.getJSONObject(i);
    			servList.add(new Automotos(json_data.getString("PLATE"), json_data.getString("DESCRIPTION"), Long.parseLong(json_data.getString("COUNTRY_ID")), json_data.getString("AUTOMOTO_GUID"),  json_data.getString("AUTOMOTO_DATEREC")));
    		}

    		return servList;
        } catch (IOException e) {
            e.printStackTrace();
        }

        return null;
	}
```

origin - http://www.pipiscrew.com/?p=2081 php-httppost-minimal