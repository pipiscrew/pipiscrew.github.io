---
title: TransactionScope
author: PipisCrew
date: 2019-03-02
categories: [.net]
toc: true
---

```js
//https://docs.microsoft.com/en-us/dotnet/api/system.transactions.transactionscope?view=netframework-4.0
try
{
    using (TransactionScope scope = new TransactionScope())
    {
        // Do Operation 1
        // Do Operation 2
        //...

        // if all the coperations complete successfully, this would be called and commit the trabsaction. 
        // In case of an exception, it wont be called and transaction is rolled back
        scope.Complete();
    }
}
catch (ThreadAbortException ex)
{
    // Handle exception
}
```

* * *

You should use TransactionScope because of the flexibility it provides. It will make it easier in the future to include things other than ADO.NET calls into a transaction.

## SqlTransaction 

```js
//https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqltransaction?view=netframework-4.0
using (SqlTransaction tran = conn.BeginTransaction())
{
	try
	{
		// Insert into File Registry
		using (SqlCommand cmd = new SqlCommand(fileQuery, conn, tran))
		{
			String[] parts = article.DocumentFileLink.Split('/');
			String file = parts[parts.Length - 1];
			String filename = "News/" + file;
			cmd.Parameters.AddWithValue("@UploadedFileName", file);
			cmd.Parameters.AddWithValue("@FileName", filename);
			cmd.Parameters.AddWithValue("@FileUrl", article.DocumentFileLink);

			Int64 id = (Int64)cmd.ExecuteScalar();

			SqlCommand cmd2 = new SqlCommand(artFileQuery, conn, tran);
			cmd2.Parameters.AddWithValue("@ArticleID", article.ID);
			cmd2.Parameters.AddWithValue("@FileRegistryID", id);
			cmd2.ExecuteScalar();

		}
		tran.Commit();
	}
	catch (Exception ex)
	{
		tran.Rollback();
		// throw;
	}
	finally
	{
		TaskBucket.completedTasks.Add(article.ID);
		if (conn.State == ConnectionState.Open)
		{
			conn.Close();
		}
	}
}
```

origin - https://www.pipiscrew.com/?p=14718 transactionscope