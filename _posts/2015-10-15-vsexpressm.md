---
title: o[vsexpress+mysql] asp.net using entity framework with mysql on visual studio express (old)
author: PipisCrew
date: 2015-10-15
categories: [sql,.net,asp.net,linq]
toc: true
---

reference 
http://www.rssbus.com/kb/articles/ado-entityframework-manual.rst
https://msdn.microsoft.com/en-us/library/bb896270(v=vs.100).aspx
https://social.msdn.microsoft.com/Forums/en-US/e2d6f829-0703-47cc-b23a-25f563c25712/adonet-entity-framwork-the-specified-metadata-path-is-not-valid?forum=adodotnetentityframework

## What is Entity Framework?

[http://www.codeproject.com/Articles/676309/ADO-NET-Entity-Framework-Interview-Questions](http://www.codeproject.com/Articles/676309/ADO-NET-Entity-Framework-Interview-Questions)

> the problem: cant use mysql-connector doesnt appear on connection dialog!!

VSExpress users continue reading the article
VSPro for 2010 you must install mysql-connector-net-6.6.5.msi, tested&working (src - http://stackoverflow.com/questions/4235291/how-to-connect-to-a-mysql-data-source-in-visual-studio)
VSPro above use MySQL for Visual Studio

![snap309](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap309.png)

1-download&install latest mysql-connector http://download.softagency.net/MySQL/Downloads/Connector-Net/ (tested with mysql-connector-net-6.9.7.msi, **tried also with mysql-connector-net-6.3.4 but failed!**)
2-run your mysql instance, you must have already a database and some tables on it
3-open cmd goto :
%windir%\Microsoft.NET\Framework\v4.0.30319\
4-execute at cmd  :
```js
edmgen.exe /provider:MySql.Data.MySqlClient /mode:fullgeneration /c:"Data Source=localhost;Initial Catalog=testdb2;User ID=x;Password=x;" /project:School /entitycontainer:SchoolEntities /namespace:SchoolModel /language:CSharp
```
^this one will generate 5files!
![snap305](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap305.png)

drop all to your project!

![snap306](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap306.png)

the tagged^ files School.csdl / School.msl / School.ssdl must have Build Action : Embedded Resource and other 2 Build Action : Compile...

![snap307](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap307.png)

then add the connection string to your web.config (you will use it on ~every page, right?) 
WARNING must append in front of csdl/ssdl/msl filenames the PRJ Namespace! example :
```js
<configuration>
    <system.web>
        <compilation debug="true" targetframework="4.0"></compilation>
      <pages enableviewstate="false"></pages>
    </system.web>
    <connectionstrings>
      <add name="SchoolEntities" connectionstring="metadata=res://*/WebApplication1.School.csdl|res://*/WebApplication1.School.ssdl|res://*/WebApplication1.School.msl;provider=MySql.Data.MySqlClient;provider connection string='Data Source=localhost;Initial Catalog=x;User ID=x;Password=x'"></add>
    </connectionstrings>
</configuration>
```

5-use [EdmGen2](http://www.softpedia.com/get/Programming/Other-Programming-Files/EdmGen.shtml) to generate the .edmx from ^4files...

then on webform1.aspx

```js
string conn = System.Configuration.ConfigurationManager.ConnectionStrings["SchoolEntities"].ConnectionString;

SchoolModel.SchoolEntities env = new SchoolModel.SchoolEntities(conn);

var queryRet = from p in env.bubbles select p;

foreach (var results in queryRet)
{
    Console.WriteLine(results.id);
}
```
5-Add reference to your VS PRJ, System.Data.Entity.dll + System.Runtime.Serialization.dll > F5!

![snap308](https://www.pipiscrew.com/wp-content/uploads/2015/10/snap308.png)

yeah is working.. :)

origin - http://www.pipiscrew.com/?p=2216 vsexpressmysql-asp-net-using-entity-framework-with-mysql-on-visual-studio-express