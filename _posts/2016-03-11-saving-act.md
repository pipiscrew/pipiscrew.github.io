---
title: Saving Activity state on Android
author: PipisCrew
date: 2016-03-11
categories: [android]
toc: true
---

source - [http://stackoverflow.com/a/151940/1320686](http://stackoverflow.com/a/151940/1320686)

You need to override onSaveInstanceState(Bundle savedInstanceState) and write the application state values you want to change to the Bundle parameter like this:

```js
@Override
public void onSaveInstanceState(Bundle savedInstanceState) {
  super.onSaveInstanceState(savedInstanceState);
  // Save UI state changes to the savedInstanceState.
  // This bundle will be passed to onCreate if the process is
  // killed and restarted.
  savedInstanceState.putBoolean("MyBoolean", true);
  savedInstanceState.putDouble("myDouble", 1.9);
  savedInstanceState.putInt("MyInt", 1);
  savedInstanceState.putString("MyString", "Welcome back to Android");
  // etc.
}

//The Bundle is essentially a way of storing a NVP ("Name-Value Pair") map, and it will get passed in to onCreate() and also onRestoreInstanceState() where you'd extract the values like this:

@Override
public void onRestoreInstanceState(Bundle savedInstanceState) {
  super.onRestoreInstanceState(savedInstanceState);
  // Restore UI state from the savedInstanceState.
  // This bundle has also been passed to onCreate.
  boolean myBoolean = savedInstanceState.getBoolean("MyBoolean");
  double myDouble = savedInstanceState.getDouble("myDouble");
  int myInt = savedInstanceState.getInt("MyInt");
  String myString = savedInstanceState.getString("MyString");
}
```

You would usually use this technique to store instance values for your application (selections, unsaved text, etc.).

* * *

## Save custom ArrayList on Android screen rotate

source - [http://stackoverflow.com/a/12503875/1320686](http://stackoverflow.com/a/12503875/1320686)
[http://stackoverflow.com/a/18548274/1320686](http://stackoverflow.com/a/18548274/1320686)

```js
public class Example extends ListActivity {
    ArrayList<myobject> list;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        if(savedInstanceState == null || !savedInstanceState.containsKey("key")) {
           //your code to fill list
        }
        else {
            list = savedInstanceState.getParcelableArrayList("key");
        }

        setListAdapter(new ArrayAdapter<myobject>(this, android.R.layout.simple_list_item_1, list));
    }

    @Override
    protected void onSaveInstanceState(Bundle outState) {
        outState.putParcelableArrayList("key", list);
        super.onSaveInstanceState(outState);
    }
}
```

```js
//MyObject.java
public class MyObject implements Parcelable {
    String color;
    String number;

    public MyObject(String number, String color) {
        this.color = color;
        this.number = number;
    }

    private MyObject(Parcel in) {
        color = in.readString();
        number = in.readString();
    }

    public int describeContents() {
        return 0;
    }

    @Override
    public String toString() {
        return number + ": " + color;
    }

    public void writeToParcel(Parcel out, int flags) {
        out.writeString(color);
        out.writeString(number);
    }

    public static final Parcelable.Creator<myobject> CREATOR = new Parcelable.Creator<myobject>() {
        public MyObject createFromParcel(Parcel in) {
            return new MyObject(in);
        }

        public MyObject[] newArray(int size) {
            return new MyObject[size];
        }
    };
}
```

## generate Parcelable by your class

[http://www.parcelabler.com/](http://www.parcelabler.com/)

* * *

## Parcelable vs Serializable

[http://www.developerphil.com/parcelable-vs-serializable/](http://www.developerphil.com/parcelable-vs-serializable/)

```js
//http://stackoverflow.com/q/16210831/1320686
//save (serialize)
save_customers(getActivity(), Frag_Settings_Customers_LIST);

//load (deserialize)
ArrayList<customers> x = load_customers(getActivity());

Log.w("w",x.get(2).getCUSTOMER_NAME());
```

```js
//source - http://stackoverflow.com/a/13393533/1320686
public static boolean save_customers(Context c, ArrayList<customers>  region) {
	try {
		FileOutputStream fos = c.openFileOutput("test.txt", Context.MODE_PRIVATE);
		ObjectOutputStream oos = new ObjectOutputStream(fos);
		oos.writeObject(region);
		oos.close();
	} catch (IOException e) {
		e.printStackTrace();
		return false;
	}

	return true;
}

public static  ArrayList<customers> load_customers(Context context) {
	try {
		FileInputStream fis = context.openFileInput("test.txt");
		ObjectInputStream is = new ObjectInputStream(fis);
		Object readObject = is.readObject();
		is.close();

		if(readObject != null && readObject instanceof ArrayList<??>) {
			return (ArrayList<customers>) readObject;
		}
	} catch (IOException e) {
		e.printStackTrace();
	} catch (ClassNotFoundException e) {
		e.printStackTrace();
	}

	return null;
}
```

```js
//example of save
General.save_obj(getActivity(),listHeader_Categories,"1.txt");
General.save_hashmap(getActivity(),listDataChild,"2.txt");

//example of load
//*arraylist*
listHeader_Categories = (ArrayList<frag_settings_categories>) General.load_obj(getActivity(), "1.txt");

if (listHeader_Categories == null)
	listHeader_Categories = new ArrayList<frag_settings_categories>();

//*hashmap*	
listDataChild = (HashMap<frag_settings_categories,></frag_settings_categories,><frag_settings_categories>>) General.load_hashmap(getActivity(), "2.txt");

if (listDataChild==null)
	listDataChild = new HashMap<frag_settings_categories,></frag_settings_categories,><frag_settings_categories>>();

-------------/\/\/\-------------------
the class MUST ##implements Serializable##

//public class Frag_Settings_Brands implements Serializable { }
-------------\/\/\/-------------------

//generic save/load on serializable + hashmap
//source - http://beginnersbook.com/2013/12/how-to-serialize-hashmap-in-java/
public static boolean save_hashmap(Context c, Object obj, String filename) {
	try {
		FileOutputStream fos = c.openFileOutput(filename, Context.MODE_PRIVATE);
		ObjectOutputStream oos = new ObjectOutputStream(fos);
		oos.writeObject(obj);
		oos.close();
	} catch (IOException e) {
		e.printStackTrace();
		return false;
	}

	return true;
}

public static HashMap<?,??> load_hashmap(Context context, String filename) {
	HashMap<?,??> map = null;
	  try
	  {
		 FileInputStream fis = new FileInputStream(filename);
		 ObjectInputStream ois = new ObjectInputStream(fis);
		 map = (HashMap) ois.readObject();
		 ois.close();
		 fis.close();
	  }catch(IOException ioe)
	  {
		 ioe.printStackTrace();
		 return null;
	  }catch(ClassNotFoundException c)
	  {
		 c.printStackTrace();
		 return null;
	  }
	  // Display content using Iterator
	  Set set = map.entrySet();
	  Iterator iterator = set.iterator();
	  while(iterator.hasNext()) {
		 Map.Entry mentry = (Map.Entry)iterator.next();
		 System.out.print("key: "+ mentry.getKey() + " & Value: ");
		 System.out.println(mentry.getValue());
	  }

	  return map;
}

public static boolean save_obj(Context c, ArrayList<??> obj, String filename) {
	try {
		FileOutputStream fos = c.openFileOutput(filename, Context.MODE_PRIVATE);
		ObjectOutputStream oos = new ObjectOutputStream(fos);
		oos.writeObject(obj);
		oos.close();
	} catch (IOException e) {
		e.printStackTrace();
		return false;
	}

	return true;
}

public static ArrayList<??> load_obj(Context context, String filename) {
	try {
		FileInputStream fis = context.openFileInput(filename);
		ObjectInputStream is = new ObjectInputStream(fis);
		Object readObject = is.readObject();
		is.close();

		if (readObject != null && readObject instanceof ArrayList<??>) {
			return (ArrayList<??>) readObject;
		}
	} catch (IOException e) {
		e.printStackTrace();
	} catch (ClassNotFoundException e) {
		e.printStackTrace();
	}

	return null;
}
```

* * *

## Pass from parent to child

source - [http://stackoverflow.com/a/2141166/1320686](http://stackoverflow.com/a/2141166/1320686)

```js
//parent
Intent i = new Intent();
i.putExtra("name_of_extra", myParcelableObject);

//child
Intent i = getIntent();
MyParcelable myParcelableObject = (MyParcelable) i.getParcelableExtra("name_of_extra");
```</frag_settings_categories></frag_settings_categories></frag_settings_categories></frag_settings_categories></customers></customers></customers></customers></myobject></myobject></myobject></myobject>

origin - http://www.pipiscrew.com/?p=4211 android-saving-activity-state-on-android