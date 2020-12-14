---
title: MongoDB Hello world!
author: PipisCrew
date: 2019-10-09
categories: [sql,.net]
toc: true
---

2018 - Working with MongoDB in .NET
[https://www.mongodb.com/blog/post/working-with-mongodb-transactions-with-c-and-the-net-framework](https://www.mongodb.com/blog/post/working-with-mongodb-transactions-with-c-and-the-net-framework)

2016 - Working with MongoDB in .NET
[https://www.codementor.io/pmbanugo/working-with-mongodb-in-net-1-basics-g4frivcvz](https://www.codementor.io/pmbanugo/working-with-mongodb-in-net-1-basics-g4frivcvz)

1-Download MongoDB -[ https://www.mongodb.com/download-center/community](https://www.mongodb.com/download-center/community) or [https://github.com/mongodb/mongo](https://github.com/mongodb/mongo). Choose the ZIP package, download & extract the files to **c:\mongodb**. Files aligned as :

<table>
<thead><tr><th>Server</th><th>mongod.exe</th></tr></thead><tbody>
 <tr><td>Router</td><td>mongos.exe</td></tr>
 <tr><td>Client</td><td>mongo.exe</td></tr>
 <tr><td>MonitoringTools</td><td>mongostat.exe, mongotop.exe</td></tr>
 <tr><td>ImportExportTools</td><td>mongodump.exe, mongorestore.exe, mongoexport.exe, mongoimport.exe</td></tr>
 <tr><td>MiscellaneousTools</td><td>bsondump.exe, mongofiles.exe, mongooplog.exe, mongoperf.exe</td></tr>
</tbody></table>

Make a new folder **c:\mongodb\dbase**. Start the server with :
```js 
//ref - https://docs.mongodb.com/v3.2/tutorial/install-mongodb-on-windows/
mongod.exe --dbpath C:\mongodb\dbase
```

![](https://i.imgur.com/kyhsHNN.jpg)

2-Download .NET driver  [https://mongodb.github.io/mongo-csharp-driver/](https://mongodb.github.io/mongo-csharp-driver/) or [https://github.com/mongodb/mongo-csharp-driver/releases/tag/v2.7.3](https://github.com/mongodb/mongo-csharp-driver/releases/tag/v2.7.3) (v2.7.3 is the last version supports framework v4.5.2)
3-Download Robomongo v1.3.1 [https://robomongo.org/](https://robomongo.org/) or [https://github.com/Studio3T/robomongo/releases](https://github.com/Studio3T/robomongo/releases)

![](https://i.imgur.com/1eKfwTP.png)
ref - [https://docs.mongodb.com/manual/reference/default-mongodb-port/](https://docs.mongodb.com/manual/reference/default-mongodb-port/)

<table>
<thead><tr><th>27017</th><th>The default port for mongod and mongos instances. You can change this port with port or --port.</th></tr></thead><tbody>
 <tr><td>27018</td><td>The default port for mongod when running with --shardsvrcommand-line option or the shardsvr value for the clusterRole setting in a configuration file.</td></tr>
 <tr><td>27019</td><td>The default port for mongod when running with --configsvrcommand-line option or the configsvr value for the clusterRole setting in a configuration file.</td></tr>
</tbody></table>

![](https://i.imgur.com/JZsb9VS.png)

![](https://i.imgur.com/rOiezcC.png)

4-Add the MongoDB Driver DLLs as reference to your project and paste the following :
```js
//FYI - MongoClient object is thread safe, so you can put it in a static field – 
//https://www.codementor.io/pmbanugo/working-with-mongodb-in-net-1-basics-g4frivcvz
IMongoDatabase db;

private void button1_Click(object sender, EventArgs e)
{
	try
	{
		var connectionString = "mongodb://localhost:27017";

		MongoClient client = new MongoClient(connectionString);

		db = client.GetDatabase("SignatureErrors");
	}
	catch (Exception x)
	{
		MessageBox.Show(x.Message);
	}
}

private void button2_Click(object sender, EventArgs e)
{
	var document = new BsonDocument();
	document.Add("name", "Steven Johnson");
	document.Add("age", 23);
	document.Add("subjects", new BsonArray() { "English", "Mathematics", "Physics" });

	IMongoCollection<bsondocument> collection = db.GetCollection<bsondocument>("SignatureErrorsRECS");
	collection.InsertOneAsync(document);
}
```

* * *

```js
//backup
mongoexport -d testdb -c movies -o movies.json

//restore
mongoimport -d testdb -c movies2 --file movies.json
```</bsondocument></bsondocument>

origin - https://www.pipiscrew.com/?p=14907 mongodb-hello-world