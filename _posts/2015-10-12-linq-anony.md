---
title: linq anonymous method
author: PipisCrew
date: 2015-10-12
categories: [sql,.net]
toc: true
---

reference 
[https://code.msdn.microsoft.com/101-LINQ-Samples-3fb9811b](https://code.msdn.microsoft.com/101-LINQ-Samples-3fb9811b)
[https://msdn.microsoft.com/en-us/library/bb386921(v=vs.110).aspx](https://msdn.microsoft.com/en-us/library/bb386921(v=vs.110).aspx)

```js
CREATE TABLE [CMS_Tablets](
	[Tablet_ID] [int] IDENTITY(1,1) NOT NULL,
	[Tablet_Title] [nvarchar](50) NULL,
	[Tablet_Type] [tinyint] NULL,
	[Site_ID] [int] NOT NULL,
 CONSTRAINT [PK_CMS_Tablets] PRIMARY KEY CLUSTERED
```

a function returns a datatable from dbase
```js
        public DataTable GetDATATABLE(string SQLSTR)
        {
            SqlDataAdapter sqlAD = new SqlDataAdapter();
            DataTable sqlSET = new DataTable();
            SqlCommand sqlco = new SqlCommand();

            try
            {
                sqlco.CommandText = SQLSTR;
                sqlco.Connection = objConn;

                sqlAD.SelectCommand = sqlco;
                //sqlAD.MissingSchemaAction = MissingSchemaAction.AddWithKey;
                sqlAD.Fill(sqlSET);

                return sqlSET;

            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLClass - GetDATATABLE");
                return null;
            }
            finally
            {
                sqlco.Dispose();
                sqlAD.Dispose();
                sqlSET.Dispose();
            }
        }
```

## LiNQ Example - Database to Enumerable - Select all records with order by descending

![snap072](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap072.png)

```js
//get an enumerable
IEnumerable<datarow> dt = db.GetDATATABLE("select * from [CMS_Tablets] order by [Tablet_Title]").AsEnumerable();

var products =
	   from cust in dt 
	   orderby cust.Field<string>("Tablet_Title") descending
	   where cust.Field<string>("Tablet_Title").IndexOf("ASUS") > -1 
	   select cust;

//count items 
txt_count.Text = products.Count().ToString();

//foreach item, print "Tablet_Title" field
foreach (DataRow w in products)
{
	textBox1.Text += w["Tablet_Title"] + "\r\n";
}
```

## LiNQ Example - Database to Enumerable - Group By

![snap075](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap075.png)

```js
var productGroups =
	   from p in dt
	   group p by p.Field<int>("Site_ID") into g
	   select new { Site = g.Key, Products = g };

txt_count.Text = productGroups.Count().ToString();
foreach (var w in productGroups)
{
   textBox1.Text += w.Products.FirstOrDefault().Field<int>("Site_ID") + "\r\n";
}
```

![snap076](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap076.png)
this one returns all **CMS_Tablets** group by **Site_ID** (a foreign table, has just a two records)... 

![snap077](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap077.png)
on each **Site** have **products** (a bunch of)  **datarows** where these contains the SQL Table fields.

* * *

```js
//(System.Data.DataSetExtensions.dll)
IEnumerable<datarow> dt = db.GetDATATABLE("select * from [CMS_Tablets] order by [Tablet_Title]").AsEnumerable();

//(System.Core.dll)
IEnumerable<datarow> rows = db.GetDATATABLE("select * from [CMS_Tablets] order by [Tablet_Title]").Rows.OfType<datarow>();

//source http://stackoverflow.com/a/529843
```</datarow></datarow></datarow></int></int></string></string></datarow>

origin - http://www.pipiscrew.com/?p=2151 net-linq-anonymous-method