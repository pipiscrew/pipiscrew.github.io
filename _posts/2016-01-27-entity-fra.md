---
title: Entity Framework
author: PipisCrew
date: 2016-01-27
categories: [sql,.net,linq]
toc: true
---

guide :
[http://weblogs.asp.net/scottgu/code-first-development-with-entity-framework-4](http://weblogs.asp.net/scottgu/code-first-development-with-entity-framework-4)

## Entity Framework vs LINQ to SQL

![4q3b1](https://www.pipiscrew.com/wp-content/uploads/2015/10/4q3b1.png)

source [http://stackoverflow.com/a/32319137/1320686](http://stackoverflow.com/a/32319137/1320686)

LINQ to SQL - Created by C# team
Entity Framework - Created by SQL Server team

> Sqlmetal.exe generated file is used in Linq to SQL (ORM)
> where
> EDMGen.exe tool generated file is used in EntityFramework (ORM).

source [http://stackoverflow.com/a/8641555/1320686](http://stackoverflow.com/a/8641555/1320686)

## Microsoft Entity Framework (Part1 of 6)

 by thousandtyone
[https://www.youtube.com/watch?v=BS6IKdUd2V8](https://www.youtube.com/watch?v=BS6IKdUd2V8) 

* * *

![snap473](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap473.png)

![snap474](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap474.png)

![snap475](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap475.png)

![snap476](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap476.png)

sample of 'code behind' :
```js
string conn = System.Configuration.ConfigurationManager.ConnectionStrings["testEntities"].ConnectionString;
testEntities x = new testEntities(conn);
var queryRet = (from p in x.customers select p).Take(100);

foreach (var results in queryRet)
{
	Console.WriteLine(results.eponimo);
}
```

* * *

James DeMeuse wrote ([http://stackoverflow.com/a/28353126](http://source)) :

> I hate to dump on EF because it works so well, but it is just slow. In most cases I just want to find a record or update/insert. Even simple operations like this are slow. I pulled back 1100 records from a table into a List and that operation took 6 seconds with EF. For me this is too long, even saving takes too long.
> 
> I ended up making my own ORM. I pulled the same 1100 records from a database and my ORM took 2 seconds, much faster than EF. Everything with my ORM is almost instant.

[https://github.com/jdemeuse1204/OR-M-Data-Entities](https://github.com/jdemeuse1204/OR-M-Data-Entities)

[http://ormdataentities.com/](http://ormdataentities.com/)

origin - http://www.pipiscrew.com/?p=2179 entity-framework