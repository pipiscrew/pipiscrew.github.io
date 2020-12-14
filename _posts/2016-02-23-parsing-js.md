---
title: Parsing JSON
author: PipisCrew
date: 2016-02-23
categories: [android]
toc: true
---

```js
//For example in Gson, if you have got a class named Car built in this way:
class Car{
  int wheels;
  String plate;
}

//... and you want to parse an array of cars, you can easily inflate your JSON in this way:
Gson gson = new Gson;
List<car> cars = gson.fromJson(input, new TypeToken<><car>>(){}.getType());
```

[http://stackoverflow.com/a/10097257](http://stackoverflow.com/a/10097257)

## Gson vs Jackson: Which to Use for JSON in Java

[http://www.doublecloud.org/2015/03/gson-vs-jackson-which-to-use-for-json-in-java/](http://www.doublecloud.org/2015/03/gson-vs-jackson-which-to-use-for-json-in-java/)

[https://dzone.com/articles/be-lazy-productive-android](https://dzone.com/articles/be-lazy-productive-android)

* * *

## Jackson json2class

```js
//source - http://stackoverflow.com/a/24231305/1320686
  //create ObjectMapper instance
    ObjectMapper objectMapper = new ObjectMapper();

    //convert json string to object
    Employee emp = objectMapper.readValue(jsonData, Employee.class); 
```

## gson josn2class

You can use gson.jar to store class objects into SharedPreferences. You can downlaod this jar from here https://github.com/google/gson

```js
//source - http://stackoverflow.com/a/18463758/1320686
//Or add GSON dependency in Gradle file -- build.app -- compile 'com.google.code.gson:gson:2.5'

//Creating a shared preference
SharedPreferences  mPrefs = getPreferences(MODE_PRIVATE);
To Save

     Editor prefsEditor = mPrefs.edit();
     Gson gson = new Gson();
     String json = gson.toJson(MyObject);
     prefsEditor.putString("MyObject", json);
     prefsEditor.commit();
To Retreive

    Gson gson = new Gson();
    String json = mPrefs.getString("MyObject", "");
    MyObject obj = gson.fromJson(json, MyObject.class);
```</car></car>

origin - http://www.pipiscrew.com/?p=3703 android-parsing-json