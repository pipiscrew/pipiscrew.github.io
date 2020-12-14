---
title: Nick Chamberlain - Calculating Values Using Calculated Values In LINQ
author: PipisCrew
date: 2016-01-04
categories: [.net]
toc: true
---

Author : Nick Chamberlain 
Source : [http://www.c-sharpcorner.com/UploadFile/46a477/calculating-values-using-calculated-values-in-linq/](http://www.c-sharpcorner.com/UploadFile/46a477/calculating-values-using-calculated-values-in-linq/)

[https://github.com/heynickc/linq_subexpressions/blob/master/LinqSubexpressions/DoubleIteration.cs](https://github.com/heynickc/linq_subexpressions/blob/master/LinqSubexpressions/DoubleIteration.cs)

Need to perform a LINQ query with a calculated value that relies on the result of another calculated value?
```js
using(MyDbContext db = new MyDbContext())  
{  
    var data = db.SomeTable  
        .Where(x => x.Id = "SomeId")  
        .Select(x => new  
            {  
            x.Field1,  
                x.Field2,  
                x.Field3,  
                CalculatedField = Calculation(  
                    x.Field1,  
                    x.Field2,  
                    x.Field3),  
                AnotherCalculatedField = AnotherCalculation(  
                    CalculatedField,  
                    x.Field1,  
                    x.Field2,  
                    x.Field3),  
        }).ToList();  
    return data;  
}  
```

This will throw: The name 'CalculatedField' does not exist in the current context. To compile, we can use the method as a parameter.
```js
AnotherCalculatedField = AnotherCalculation  
(  
    Calculation(x.Field1, x.Field2, x.Field3),  
    x.Field1,  
    x.Field2,  
    x.Field3  
)
```

I'll use Serilog and SerilogMetrics (see `counter.Increment()` above) to get some metrics. In our query, we'll calculate a LineTotal field in a projected anonymous type, calling the slow CalculateLinePrice() method above.
```js
using(var db = new FakeMyDbContext())  
{  
    var sods = new List < salesorderdetail=""> ();  
    for (int i = 0; i < 10;="" i++)="" {="" sods.add(new="" salesorderdetail()="" {="" salesorderid="71774," productid="905," orderqty="4," unitprice="218.454" m="" });="" }="" db.salesorderdetails.addrange(sods);="" using(log.logger.begintimedoperation("calculating="" quick="" total"))="" {="" _calclinepricecounter.reset();="" var="" results="db.SalesOrderDetails" .where(sod=""> sod.SalesOrderId == 71774)  
            .ToList()  
            .Select(sod => new  
                {  
                sod.OrderQty,  
                    sod.UnitPrice,  
                    LineTotal = CalculateLinePrice(  
                        sod.OrderQty,  
                        sod.UnitPrice,  
                        _calcLinePriceCounter)  
            }).ToList();  
        _calcLinePriceCounter.Write();  
    }  
}
```

Since there are 10 * SalesOrderDetail in FakeMyDbContext, this will take around 10 * 500 = 5000 milliseconds. 
-Beginning operation "Test": "Calculating quick total".
-"CalculateLinePrice Counter" count = 10 operation(s).
-Completed operation "Test": "Calculating quick total".
-in 00:00:05.0020498 (5002 ms).

Not bad, until we want to use LineTotal for another calculation.

### Complicating Things

The problem happens when we need to use LineTotal as a parameter for another calculation. We'll add 2 more methods to calculate margin:
```jspublic decimal CalculateLinePrice(short qty, decimal unitPrice, ICounterMeasure counter)  
{  
    Thread.Sleep(500);  
    counter.Increment();  
    return qty * unitPrice;  
}  
We need to pass the results of CalculateLineCost() and CalculateLinePrice() into CalculateMargin(decimal lineCost, decimal linePrice):
using(var db = new FakeMyDbContext())  
{  
    var sods = new List < salesorderdetail=""> ();  
    for (int i = 0; i < 10;="" i++)="" {="" sods.add(new="" salesorderdetail()="" {="" salesorderid="71774," productid="905," orderqty="4," unitprice="218.454" m="" });="" }="" db.salesorderdetails.addrange(sods);="" using(log.logger.begintimedoperation("calculating="" quick="" total"))="" {="" _calclinepricecounter.reset();="" var="" results="db.SalesOrderDetails" .where(sod=""> sod.SalesOrderId == 71774)  
            .ToList()  
            .Select(sod => new   
               {  
                sod.OrderQty,  
                    sod.UnitPrice,  
                    LineTotal = CalculateLinePrice(  
                        sod.OrderQty,  
                        sod.UnitPrice,  
                        _calcLinePriceCounter)  
            }).ToList();  
        _calcLinePriceCounter.Write();  
    }  
}  
```

Now, we're calling the pricing methods 20 times each! At 500 ms, this comes to 20024 ms total.
-Beginning operation "Test": "Calculating margin slowly".
-"CalculateLinePrice Counter" count = 20 operation(s).
-"CalculateLineCost Counter" count = 20 operation(s).
-"CalculateMargin Counter" count = 10 operation(s).
-Completed operation "Test": "Calculating margin slowly".
-in 00:00:20.0249976 (20024 ms).

### LINQ Sub-Expressions

We could calculate the intermediate values with one iteration, then the margin value with another iteration of the collection, but that's not efficient.
A better solution is to use LINQ sub-expressions.
"In a query expression it is sometimes useful to store the result of a sub-expression in order to use it in subsequent clauses" - `let` clause (MSDN)
Here's what a LINQ sub-expression looks like with the method syntax that we've been using:
```jsvar results = db.SalesOrderDetails  
    .Where(sod => sod.SalesOrderId == 71774)  
    .Join(db.Products,  
        sod => sod.ProductId,  
        product => product.ProductId,  
        (sod, product) => new   
          {  
            sod,  
            product  
        })  
    .Select(li =>  
        new {  
            lineTotal = CalculateLinePrice(  
                    li.sod.OrderQty,  
                    li.sod.UnitPrice,  
                    _calcLinePriceCounter),  
                lineCost = CalculateLineCost(  
                    li.sod.OrderQty,  
                    li.product.StandardCost,  
                    _calcLineCostCounter),  
                li  
        })  
    .Select(lineItem =>  
        new {  
            lineItem.li.sod.OrderQty,  
                lineItem.li.sod.UnitPrice,  
                lineItem.li.product.StandardCost,  
                LineTotal = lineItem.lineTotal,  
                LineCost = lineItem.lineCost,  
                Margin = CalculateMargin(  
                    lineItem.lineCost,  
                    lineItem.lineTotal,  
                    _calcMarginCounter)  
        }).ToList();  ```

If we were using query syntax, we would use the let clause. Our query would look like this:
```js
var results = (from li in  
    (from sod in db.SalesOrderDetails where sod.SalesOrderId == 71774 join product in db.Products on sod.ProductId equals product.ProductId select new  
     {  
        sod,  
        product  
    }) let lineTotal = CalculateLinePrice(  
        li.sod.OrderQty,  
        li.sod.UnitPrice,  
        _calcLinePriceCounter)  
    let lineCost = CalculateLineCost(  
        li.sod.OrderQty,  
        li.product.StandardCost,  
        _calcLineCostCounter)  
    select new   
    {  
        li.sod.OrderQty,  
            li.sod.UnitPrice,  
            li.product.StandardCost,  
            LineTotal = lineTotal,  
            LineCost = lineCost,  
            Margin = CalculateMargin(  
                lineCost,  
                lineTotal,  
                _calcMarginCounter)  
    }).ToList();  ```

You can see that the intermediate methods are only being called once per iteration, 10 times each at 10240 ms for the full query:
-Beginning operation "Test":
-"Calculating margin with subexpression".
-"CalculateLinePrice Counter" count = 10 operation(s).
-"CalculateLineCost Counter" count = 10 operation(s).
-"CalculateMargin Counter" count = 10 operation(s).
-Completed operation "Test":
-"Calculating margin with subexpression" in 00:00:10.2409290 (10240 ms).

### Summary

In this quick post, we needed to reuse a calculated value inside of a LINQ query. We didn't want to call the calculation multiple times. We also didn't want to iterate the collection twice. We found LINQ sub-expressions as a solution that allows us to stash calculated values to use in other places in our LINQ query. This allows us to call the expensive calculations once per iteration. Hope this was helpful to you, or you find it helpful in the future. There is a bonus optimization we can make to this kind of code using PLINQ. It's in the sample code (https://github.com/heynickc/linq_subexpressions) so feel free to check it out.

origin - http://www.pipiscrew.com/?p=3063 nick-chamberlain-calculating-values-using-calculated-values-in-linq