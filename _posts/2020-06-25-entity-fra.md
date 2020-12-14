---
title: Entity framework LINQ w/ nested table
author: PipisCrew
date: 2020-06-25
categories: [.net,linq]
toc: true
---

Using Lambda Expression
```js
using (var context = new EntityContext())
{
    var customers = context.Customers
            .Include(i => i.Invoices.Select(it => it.Items))
            .ToList();
}
```

Using String Path
```js
using (var context = new EntityContext())
{
    var customers = context.Customers
            .Include("Invoices.Items")
            .ToList();
}
```

Also the two of them will load all customers, their related invoices, and the items of each invoice.

In **Entity Framework Core** use **.ThenInclude**
```js
//src - https://stackoverflow.com/a/47555838
//ref - https://docs.microsoft.com/en-us/ef/core/querying/related-data
var blogs = context.Blogs
    .Include(blog => blog.Posts)
        .ThenInclude(post => post.Author)
    .ToList();
```

src - https://entityframework.net/include-multiple-levels

origin - https://www.pipiscrew.com/?p=18561 entity-framework-linq-w-nested-table