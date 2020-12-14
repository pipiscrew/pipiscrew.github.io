---
title: Npgsql provider
author: PipisCrew
date: 2016-05-30
categories: [.net]
toc: true
---

Is the .NET data provider for PostgreSQL. It allows any program developed for .NET framework to access a PostgreSQL database server. It is implemented in 100% C# code.

[http://www.npgsql.org/doc/](http://www.npgsql.org/doc/)

[https://github.com/npgsql/npgsql](https://github.com/npgsql/npgsql)

```js
using (var conn = new NpgsqlConnection("Host=myserver;Username=mylogin;Password=mypass;Database=mydatabase"))
{
    conn.Open();
    using (var cmd = new NpgsqlCommand())
    {
        cmd.Connection = conn;

        // Insert some data
        cmd.CommandText = "INSERT INTO data (some_field) VALUES ('Hello world')";
        cmd.ExecuteNonQuery();

        // Retrieve all rows
        cmd.CommandText = "SELECT some_field FROM data";
        using (var reader = cmd.ExecuteReader())
        {
            while (reader.Read())
            {
                Console.WriteLine(reader.GetString(0));
            }
        }
    }
}
```

origin - http://www.pipiscrew.com/?p=5707 net-npgsql-provider