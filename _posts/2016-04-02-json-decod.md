---
title: json decode by PHP
author: PipisCrew
date: 2016-04-02
categories: [php,android]
toc: true
---

```js
//get_multi_recordset.php
$brands  = getSet($db, "select brand_id from brands where user_id=?", array($user_id));
$categories  = getSet($db, "select category_id from categories where user_id=?", array($user_id));
$subcategories  = getSet($db, "select subcategory_id from subcategories where user_id=?", array($user_id));
$payments  = getSet($db, "select payment_id from payments where user_id=?", array($user_id));

$json                = array('brands'=> $brands, 'categories' => $categories, 'subcategories'  => $subcategories, 'payments'  => $payments);

header("Content-Type: application/json", true);

echo json_encode($json);
```

```js
//here async, get the response from get_multi_recordset.php, and decode the JSONObject
try {
	JSONObject resp = new JSONObject(response);

	JSONArray brands = resp.getJSONArray("brands");

	String brand_ids="";
	for (int i = 0 ; i < brands.length();="" i++){="" brand_ids+="((JSONObject)" brands.get(i)).getstring("brand_id")="" +="" ",";="" }="" if="" (brand_ids.length()=""> 0)
		brand_ids = brand_ids.substring(0, brand_ids.length() - 1);

} catch (JSONException e) {
	// TODO Auto-generated catch block
	e.printStackTrace();
}
```

the steps :
1-PHP Send us an JSONObject , at android unwrap the first array element (aka brands)
2-Loop through #brands# array element, each array item is JSONObject!
![snap114](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap114.png)

3-use getString to get the desire value! As you see on the screenshot data comes from database so expecting a brand_id

![snap116](https://www.pipiscrew.com/wp-content/uploads/2016/04/snap116.png)

origin - http://www.pipiscrew.com/?p=4712 android-json-decode-by-php