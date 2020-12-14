---
title: LINQ Clone + Common LINQ mistakes
author: PipisCrew
date: 2020-09-23
categories: [.net,linq]
toc: true
---

> Is an object still connected to a list after FirstOrDefault?

Yes! Any change made will reflected to origin object.

FirstOrDefault selects an item in a collection, but does not clone it, it is the same instance. [src](https://stackoverflow.com/a/2436403)

example :
```js
//https://stackoverflow.com/a/52214742

var obj = myCollection.FirstOrDefault(x => x.Param == "match condition");  
if (obj != null)
{
    obj.Property = newValue; // this will reflect in your object in the original collection
}
```

* * *

### What is the solution to make a copy of and dont disturb the original object ?

Use **Object.MemberwiseClone**

```js
public partial class Form1 : Form
{
	public Form1()
	{
		InitializeComponent();
	}

	private void button1_Click(object sender, EventArgs e)
	{
		List<player> teamList = new List<player>();

		teamList.Add(new Player() { Fullname = "Dave", Email = "dave@gmail.io" });
		teamList.Add(new Player() { Fullname = "Miky", Email = "miky@yahoo.io" });
		teamList.Add(new Player() { Fullname = "Sawyer", Email = "sawyer@gmail.io" });
		teamList.Add(new Player() { Fullname = "Simon", Email = "simon@yahoo.io" });

		//the following modify the original object
		Player test0 = teamList.FirstOrDefault(x => x.Fullname.Equals("dave", StringComparison.OrdinalIgnoreCase));
		test0.Email = "lollapalooza";

		List<player> yahooUsers = teamList.Where(x => x.Email.Contains("yahoo")).ToList();
		yahooUsers[0].Email = "ABC";
		////////

		//using MemberwiseClone is just a clone 
		Player test1 = teamList.FirstOrDefault(x => x.Fullname.Equals("dave", StringComparison.OrdinalIgnoreCase)).CloneItem();
		test1.Email = "modified";

		IList<player> gmailUsers = teamList.Where(x => x.Email.Contains("gmail")).ToList().Clone();
		gmailUsers[0].Email = "bazoo";
		////////

		Console.WriteLine("press any key");
	}

	private class Player : ICloneable
	{
		public string Fullname { get; set; }
		public string Email { get; set; }

		public object Clone()
		{
			return this.MemberwiseClone();
		}

		public Player CloneItem()
		{
			return (Player) this.MemberwiseClone();
		}

	}
}

public static class ext
{
	public static IList<t> Clone<t>(this IList<t> listToClone) where T : ICloneable
	{   // src - https://stackoverflow.com/a/222640
	    return listToClone.Select(item => (T)item.Clone()).ToList();
	}
}

```

**refs:**
https://stackoverflow.com/a/21119212
https://docs.microsoft.com/en-us/dotnet/api/system.object.memberwiseclone

* * *

## SanderSade - Common LINQ mistakes

```js
//src - https://github.com/SanderSade/common-linq-mistakes

//Incorrect:
var person = persons.Where(x => x.LastName == "Smith" && x.FirstName == "John").First();

//Correct:
var person = persons.First(x => x.LastName == "Smith" && x.FirstName == "John");

//Incorrect:
var person = persons.SingleOrDefault(x => x.Id == 21034);

//Correct:
var person = persons.FirstOrDefault(x => x.Id == 21034);
Explanation
Single()/SingleOrDefault() ensures that there is just one and only one match in the set, whereas First()/FirstOrDefault() returns the first match.

//Incorrect:
if (persons.Count() > 0)...
if (persons.Count(x => x.LastName == "Smith") > 0)...
if (persons.Count(x => x.LastName == "Smith") == persons.Count())...

//Correct:
if (persons.Any())...
if (persons.Any(x => x.LastName == "Smith"))...
if (persons.All(x => x.LastName == "Smith"))...

//Incorrect:
persons.Where(x => x.LastName == "Smith").Where(x => x.FirstName == "John");

//Correct:
persons.Where(x => x.LastName == "Smith" && x.FirstName == "John");

//Incorrect:
persons.OrderBy(x => x.LastName).OrderBy(x => x.FirstName);

//Correct:
persons.OrderBy(x => x.LastName).ThenBy(x => x.FirstName);

//Incorrect:
persons.Where(x => x.LastName == "Smith" && x.FirstName == "John").Select(x => x);

//Correct:
persons.Where(x => x.LastName == "Smith" && x.FirstName == "John");

//Incorrect:
var employees = persons.Where(x => x is Employee).Select(x => x as Employee);
var employees = persons.Where(x => x is Employee).Select(x => (Employee)x);
var employees = persons.Select(x => x as Employee).Where(x => x != null);

//Correct:
var employees = persons.OfType<employee>();

//Incorrect:
var count = peopleArray.Count();
var count = peopleList.Count();
var count = peopleDictionary.Count();

//Correct:
var count = peopleArray.Length;
var count = peopleList.Count;
var count = peopleDictionary.Count;

//////////////////////////// MERGED
//group by multiple (two) cols
var groupRows = teamList.Where(x => !string.IsNullOrEmpty(x.Email)).GroupBy(x => x.Domain, x => x.Language,
		(key, g) => new { Table = key, Languages = g.ToList().Distinct() });

//for nullable variables, use to avoid "'Operator '&&' cannot be applied to operands of type 'bool' and 'bool?'"
.Any(x => x.IsMultilingual.GetValueOrDefault() && x.Id==1)

//compare type from string
(Type.GetType("System.Int32") == typeof(Int32))

```

#linq #groupby #copy</employee></t></t></t></player></player></player></player>

origin - https://www.pipiscrew.com/?p=19082 linq-clone-common-linq-mistakes