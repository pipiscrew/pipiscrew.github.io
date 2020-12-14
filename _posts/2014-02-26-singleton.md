---
title: Singleton
author: PipisCrew
date: 2014-02-26
categories: []
toc: true
---

**Singleton class :**

```js
	public class MySingleton {
		private static volatile MySingleton instance = null;
		private String baseURL;

		// private constructor
		private MySingleton() {
		}

		public static MySingleton getInstance() {
			if (instance == null) {
				synchronized (MySingleton.class) {
					// Double check
					if (instance == null) {
						instance = new MySingleton();
					}
				}
			}
			return instance;
		}

		public void customSingletonMethod()
		{
			// Custom method
		}

		public String getBaseURL() {
		       return baseURL;
		}

		public void setBaseURL(String baseURL) {
		       this.baseURL = baseURL;
		}
	}
```

**<span style="color: #ff0000;">by Lokesh Gupta</span>** [original article](http://howtodoinjava.com/2012/10/22/singleton-design-pattern-in-java/)

> Please ensure to use **“volatile”** keyword with instance variable otherwise you can run into out of order write error scenario, where reference of instance is returned before actually the object is constructed i.e. JVM has only allocated the memory and constructor code is still not executed. In this case, your other thread, which refer to uninitialized object may throw null pointer exception and can even crash the whole application.
> 
> **//Double check** : Suppose there are two threads T1 and T2. Both comes to create instance and execute “instance==null”, now both threads have identified instance variable to null thus assume they must create an instance. They sequentially goes to synchronized block and create the instances. At the end, we have two instances in our application.

**Application class :**

```js
	public class MyApplication extends Application
	{
	  @Override
	  public void onCreate()
	  {
	    super.onCreate();

	    // Initialize the singletons so their instances
	    // are bound to the application process.
	    initSingletons();
	  }

	  protected void initSingletons()
	  {
	    // Initialize the instance of MySingleton
	    MySingleton.getInstance();
	    .
	    .
	    YourSingleton.getInstance();
	  }

	}
```

**At AndroidManifest.xml :**

```js
application android:icon="@drawable/icon" android:label="@string/app_name"
	    android:name=".MyApplication"

```

**Use on all classes :**
```js
MySingleton.getInstance().setBaseURL("https://pipiscrew.com");
.
.
MySingleton.getInstance().customSingletonMethod();
.
.
MySingleton.getInstance().getBaseURL();
```

**<span style="color: #ff0000;">by Andrea Bresolin</span>** [original article](http://www.devahead.com/blog/2011/06/extending-the-android-application-class-and-dealing-with-singleton/)

The **getInstance** method lets the internal instance be initialized only once and this is done in the MyApplication class. At this point you may ask: "wait a moment… why is the singleton initialized in MyApplication??? Isn’t it supposed to be just a singleton so the instance can be initialized everywhere in the application like in an Activity?" Here comes the tricky part…

I found that sometimes some **static variables** bound to activities happened to be **uninitialized** even though they’ve previously been initialized! **I thought that when a static variable is initialized it stays so for the entire life of the application**, but this doesn’t seem to be the case. Among all the information I found on the web, I tried to find out a safe and reliable way to initialize static variables (and you know that the singleton design pattern requires the use of a static variable). The explanation of the weird behavior I saw that makes more sense to me is that the static variables instances are bound to the class loader of the class that first initialized them. So what does this mean? This means that if a static variable inside any class has been initialized by an activity, when that activity is destroyed also its class might be unloaded and so **the variable becomes uninitialized again!** While if the variable is initialized by the application class, it’s life is the same as the application process so we’re sure that it will never become uninitialized again. That’s why I chose to initialize all the singletons in the MyApplication class.

origin - http://www.pipiscrew.com/?p=872 android-singleton