---
title: IQueryable and TSQL
author: PipisCrew
date: 2016-05-04
categories: [sql,.net]
toc: true
---

source - [http://www.mortenanderson.net/logging-sql-statements-in-entity-framework](http://www.mortenanderson.net/logging-sql-statements-in-entity-framework)

If you want to see how your LINQ query is going to look like when tranformed into SQL all you have to do is call ToString() on your IQueryable

Running the example below
```js
using (var context = new PersonDbContext())
{
    var query = context.Persons.Where(x => x.Age == 34);
    Console.WriteLine(query.ToString());
}
```

Will output

```js
SELECT 
[Extent1].[Id] AS [Id], 
[Extent1].[FirstName] AS [FirstName], 
[Extent1].[LastName] AS [LastName], 
[Extent1].[Age] AS [Age]
FROM [dbo].[People] AS [Extent1]
WHERE 34 = [Extent1].[Age]
```

origin - http://www.pipiscrew.com/?p=5184 iqueryable-and-tostring