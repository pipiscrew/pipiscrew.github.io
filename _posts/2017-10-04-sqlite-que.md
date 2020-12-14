---
title: sqlite query datetime between
author: PipisCrew
date: 2017-10-04
categories: [android,.net]
toc: true
---

```js
//tested platform : android
//at dbase the field is TEXT, queries like :
/*
select count(ordertype) as c,ordertype from orders 
where daterec between '2017-05-20 00:00:00' and '2017-05-21 23:59'
group by ordertype order by ordertype

select *  from orders 
where daterec between '2017-05-20 00:00' and '2017-05-21 23:59'
*/

		Date dtp_today = new Date();
		Date dtp_start = new Date(dtp_today.getYear(), dtp_today.getMonth(),1);
		Date dtp_end = new Date(dtp_today.getYear(), dtp_today.getMonth()+1,1);

		String str_start = new SimpleDateFormat("yyyy-MM-dd 00:00").format(dtp_start);
		String str_end = new SimpleDateFormat("yyyy-MM-dd 23:59").format(dtp_end);

		Cursor c = get_count_of_orders(str_start, str_end);

	public Cursor get_count_of_orders(String start,String end){
		Cursor c = database
				.rawQuery("select count(ordertype) as c,ordertype from orders where daterec between '" + start + "' and '" + end + "' group by ordertype order by ordertype",	null); 
		c.moveToFirst();

		return c;
	}

//save the date field as :
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm");
		txtDaterec.setText(sdf.format(new Date()));
```

using C# and Fiscal lib (http://adodotnetsqlite.sourceforge.net/), when the date field saved **yyyy-MM-dd** without timestamp you can use the between without problems. 

Saving the field as datetime **yyyy-MM-dd HH:mm** and using the same technic^ as java does not return any record. 

The trick applies also to another languages not only to C#, we will use the sqlite builtin function **strftime**. 

Of course instead you can save the field as UTC then always you have to do conversion from your program before query. Anyway we want the data to be stored as **yyyy-MM-dd HH:mm** and query as it.

```js
--https://sqlite.org/datatype3.html

CREATE TABLE "main"."test_tbl" (
"id"  INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
"date_stamp"  TEXT
)
```

```js
string now = DateTime.Today.ToString("yyyy-MM-dd");
DataTable dT = db.GetDATATABLE("select * from test_tbl where " +
"strftime('%s',date_stamp) between strftime('%s','" + now + " 00:00:00') " +
"and " +
"strftime('%s','" + now + " 23:59:00')");
```

```js
strftime('%s' = converts the given date to UTC format
```

when executing the following code :
```js
string now = DateTime.Today.ToString("yyyy-MM-dd");
DataTable dT = db.GetDATATABLE("select strftime('%s',date_stamp),date_stamp from test_tbl");
dataGridView1.DataSource = dT;
```

![alt](https://i.imgur.com/UGWrGsm.png)

```js
//adding record to dbase
SQLiteParameter parameter = null;
SQLiteCommand command = new SQLiteCommand("INSERT INTO test_tbl (date_stamp) " +
	" values (@date_stamp)", db.GetConnection());

parameter = command.CreateParameter();
parameter.ParameterName = "@date_stamp"; //valid @ DBNull.Value;
parameter.Value = DateTime.Now.ToString("yyyy-MM-dd HH:mm");
command.Parameters.Add(parameter);

command.ExecuteNonQuery();
```

> %d		day of month: 00
> %f		fractional seconds: SS.SSS
> %H		hour: 00-24
> %j		day of year: 001-366
> %J		Julian day number
> %m		month: 01-12
> %M		minute: 00-59
> %s		seconds since 1970-01-01
> %S		seconds: 00-59
> %w		day of week 0-6 with Sunday==0
> %W		week of year: 00-53
> %Y		year: 0000-9999
> %%		%

src - [https://sqlite.org/lang_datefunc.html](https://sqlite.org/lang_datefunc.html)

src - http://www.onlineconversion.com/unix_time.htm

origin - http://www.pipiscrew.com/?p=8307 sqlite-query-datetime-between