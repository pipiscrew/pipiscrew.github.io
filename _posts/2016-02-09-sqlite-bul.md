---
title: o[sqlite] bulk insert 16000 rows in 5seconds
author: PipisCrew
date: 2016-02-09
categories: [sql,.net]
toc: true
---

```js
//sqlite dll - http://system.data.sqlite.org/downloads/1.0.84.0/sqlite-netFx45-setup-bundle-x86-2012-1.0.84.0.exe
SQLClass connS;
SQLiteClass conn;

private void Form1_Load(object sender, EventArgs e)
{
	conn = new SQLiteClass("Data Source=dbase.db3;Pooling=true;FailifMissing=false;");
	string tbl = "create table products ( id integer primary key autoincrement, Product_Code text, Product_ID text, CategoryCaption_Title text, ProductCaption_Title text, ManufacturerCaption_Title text, AvailabilityText text, AvailabilityImage text)";

	if (conn.ExecuteNonQuery(tbl) == 0)
		label5.Visible = true;

	System.Data.SqlClient.SqlException error = null;

	connS = new SQLClass(txtConnection.Text, out error);

	if (error != null)
	{
		MessageBox.Show(error.Message, Application.ProductName);
		return;
	}
	else
	{
		label4.Visible = true;

	}
}

SqlDataReader dr = connS.GetDATAREADER(winForm1.Properties.Resources.insert_sqlserver_to_sqlite);

var tran1 = conn.GetConnection().BeginTransaction();

using (SQLiteCommand cmd = new SQLiteCommand("insert into products (Product_Code , Product_ID, CategoryCaption_Title , ProductCaption_Title , ManufacturerCaption_Title,AvailabilityText, AvailabilityImage) values (@Product_Code , @Product_ID, @CategoryCaption_Title , @ProductCaption_Title , @ManufacturerCaption_Title, @AvailabilityText, @AvailabilityImage)", conn.GetConnection()))
{
	SQLiteParameterCollection Params = cmd.Parameters;

	while (dr.Read())
	{
		Params.Clear();

		Params.Add(new SQLiteParameter("@Product_Code", dr["PRODUCT_CODE"]));
		Params.Add(new SQLiteParameter("@Product_ID", dr["Product_ID"]));
		Params.Add(new SQLiteParameter("@CategoryCaption_Title", dr["CategoryCaption_Title"]));
		Params.Add(new SQLiteParameter("@ProductCaption_Title", dr["ProductCaption_Title"]));
		Params.Add(new SQLiteParameter("@ManufacturerCaption_Title", dr["ManufacturerCaption_Title"]));
		Params.Add(new SQLiteParameter("@AvailabilityText", null));
		Params.Add(new SQLiteParameter("@AvailabilityImage", null));

		cmd.Prepare();
		cmd.ExecuteScalar();
	}
}
tran1.Commit();

MessageBox.Show("Insert done!");
```

```js
//the SQLite class
using System;
using System.Windows.Forms;
using System.Data;
using System.Collections.Generic;
using System.Data.SQLite;

namespace PipisCrew.Classes
{
    internal class SQLiteClass
    {

        private SQLiteConnection objConn;
        private string m_ConnectionString;

        public SQLiteClass(string ConnectionString)
        {
            try
            {
                m_ConnectionString = ConnectionString;
                objConn = new SQLiteConnection(ConnectionString);
                objConn.Open();

            }
            catch (SQLiteException ex)
            {
                objConn = null;

            }
        }

        public bool IsConnected
        {
            get
            {
                if (objConn == null | objConn.State != ConnectionState.Open)
                {
                    return false;
                }
                else
                {
                    return true;
                }
            }
        }

        public string ConnectionString
        {
            get { return m_ConnectionString; }
        }

        public SQLiteDataAdapter GetAdapter(string SQLite)
        {
            return new SQLiteDataAdapter(SQLite, objConn);
        }

        public SQLiteCommand GetCommand(string Query)
        {
            return new SQLiteCommand(Query, objConn);
        }

        public DataSet GetDATASET(string SQLiteSTR)
        {
            SQLiteDataAdapter SQLiteAD = new SQLiteDataAdapter();
            DataSet SQLiteSET = new DataSet();
            SQLiteCommand SQLiteco = new SQLiteCommand();

            try
            {
                SQLiteco.CommandText = SQLiteSTR;
                SQLiteco.Connection = objConn;

                SQLiteAD.SelectCommand = SQLiteco;
                SQLiteAD.Fill(SQLiteSET, "tabl");
                return SQLiteSET;

            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLiteClass - GetDATASET");
                return null;
            }
            finally
            {
                SQLiteco.Dispose();
                SQLiteAD.Dispose();
                SQLiteSET.Dispose();
            }
        }

        public DataSet GetDATASET2(string SQLiteSTR,out string error)
        {
            SQLiteDataAdapter SQLiteAD = new SQLiteDataAdapter();
            DataSet SQLiteSET = new DataSet();
            SQLiteCommand SQLiteco = new SQLiteCommand();

            try
            {
                SQLiteco.CommandText = SQLiteSTR;
                SQLiteco.Connection = objConn;

                SQLiteAD.SelectCommand = SQLiteco;
                SQLiteAD.Fill(SQLiteSET, "tabl");
                error = "";
                return SQLiteSET;

            }
            catch (Exception ex)
            {
                error = ex.Message;
                return null;
            }
            finally
            {
                SQLiteco.Dispose();
                SQLiteAD.Dispose();
                SQLiteSET.Dispose();
            }
        }

        public SQLiteDataReader GetDATAREADER(string SQLiteSTR)
        {
            SQLiteDataReader SQLiteread = null;
            SQLiteCommand SQLiteco = new SQLiteCommand();
            try
            {
                SQLiteco.Connection = objConn;

                SQLiteco.CommandText = SQLiteSTR;

                SQLiteread = SQLiteco.ExecuteReader();
                return SQLiteread;

            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLiteClass - GetDATAREADER");
                return null;
            }
            finally
            {
                SQLiteco.Dispose();
                //SQLiteread.Close()
            }
        }

        public DataTable GetDATATABLE(string SQLiteSTR)
        {
            SQLiteDataAdapter SQLiteAD = new SQLiteDataAdapter();
            DataTable SQLiteSET = new DataTable();
            SQLiteCommand SQLiteco = new SQLiteCommand();

            try
            {
                SQLiteco.CommandText = SQLiteSTR;
                SQLiteco.Connection = objConn;

                SQLiteAD.SelectCommand = SQLiteco;
                //SQLiteAD.MissingSchemaAction = MissingSchemaAction.AddWithKey;
                SQLiteAD.Fill(SQLiteSET);

                return SQLiteSET;

            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLiteClass - GetDATASET");
                return null;
            }
            finally
            {
                SQLiteco.Dispose();
                SQLiteAD.Dispose();
                SQLiteSET.Dispose();
            }
        }

        public SQLiteConnection GetConnection()
        {
            return objConn;
        }

        public object ExecuteSQLiteScalar(string SQLiteSTR)
        {
            SQLiteCommand SQLiteco = new SQLiteCommand();
            try
            {
                SQLiteco.Connection = objConn;
                SQLiteco.CommandText = SQLiteSTR;
                return SQLiteco.ExecuteScalar();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLiteClass - ExecuteSQLiteScalar");
                return "";
            }
            finally
            {
                SQLiteco.Dispose();
            }
        }

        public int ExecuteNonQuery(string SQLiteSTR)
        {
            int functionReturnValue = 0;
            SQLiteCommand SQLiteco = new SQLiteCommand();
            try
            {
                SQLiteco.Connection = objConn;
                SQLiteco.CommandText = SQLiteSTR;
                return SQLiteco.ExecuteNonQuery();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLiteClass - ExecuteSQLite");
                functionReturnValue = 0;
            }
            finally
            {
                SQLiteco.Dispose();
            }
            return functionReturnValue;
        }

        public int ExecuteNonQuery(string SQLiteSTR, out SQLiteException ErrReport)
        {
            int functionReturnValue = 0;
            SQLiteCommand SQLiteco = new SQLiteCommand();
            ErrReport = null;

            try
            {

                SQLiteco.Connection = objConn;
                SQLiteco.CommandText = SQLiteSTR;

                return SQLiteco.ExecuteNonQuery();
            }
            catch (SQLiteException sEX)
            {
                ErrReport = sEX;
                functionReturnValue = 0;
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLiteClass - ExecuteSQLite");
                functionReturnValue = 0;
            }
            finally
            {
                SQLiteco.Dispose();
            }
            return functionReturnValue;
        }

        public void Close()
        {
            if ((objConn != null))
            {
                objConn.Close();
                objConn.Dispose();
            }
        }

    }

}
```

```js
//the SQLServer class
using System;
using System.Data.SqlClient;
using System.Windows.Forms;
using System.Data;
using System.Collections.Generic;

namespace PipisCrew.Classes
{
    internal class SQLClass
    {

        private SqlConnection objConn;
        private string m_ConnectionString;

        public SQLClass(string ConnectionString, out SqlException ExceptionObject)
        {
            try
            {
                m_ConnectionString = ConnectionString;
                objConn = new SqlConnection(ConnectionString);
                objConn.Open();

                ExceptionObject = null;
            }
            catch (SqlException ex)
            {
                objConn = null;
                ExceptionObject = ex;
            }
        }

        public bool IsConnected
        {
            get
            {
                if (objConn == null | objConn.State != ConnectionState.Open)
                {
                    return false;
                }
                else
                {
                    return true;
                }
            }
        }

        public string ConnectionString
        {
            get { return m_ConnectionString; }
        }

        public SqlDataAdapter GetAdapter(string sql)
        {
            return new SqlDataAdapter(sql, objConn);
        }

        public SqlCommand GetCommand(string Query)
        {
            return new SqlCommand(Query, objConn);
        }

        public DataSet GetDATASET(string SQLSTR)
        {
            SqlDataAdapter sqlAD = new SqlDataAdapter();
            DataSet sqlSET = new DataSet();
            SqlCommand sqlco = new SqlCommand();

            try
            {
                sqlco.CommandText = SQLSTR;
                sqlco.Connection = objConn;

                sqlAD.SelectCommand = sqlco;
                sqlAD.Fill(sqlSET, "tabl");
                return sqlSET;

            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLClass - GetDATASET");
                return null;
            }
            finally
            {
                sqlco.Dispose();
                sqlAD.Dispose();
                sqlSET.Dispose();
            }
        }

        public DataSet GetDATASET2(string SQLSTR,out string error)
        {
            SqlDataAdapter sqlAD = new SqlDataAdapter();
            DataSet sqlSET = new DataSet();
            SqlCommand sqlco = new SqlCommand();

            try
            {
                sqlco.CommandText = SQLSTR;
                sqlco.Connection = objConn;

                sqlAD.SelectCommand = sqlco;
                sqlAD.Fill(sqlSET, "tabl");
                error = "";
                return sqlSET;

            }
            catch (Exception ex)
            {
                error = ex.Message;
                return null;
            }
            finally
            {
                sqlco.Dispose();
                sqlAD.Dispose();
                sqlSET.Dispose();
            }
        }

        public SqlDataReader GetDATAREADER(string SQLSTR)
        {
            SqlDataReader sqlread = null;
            SqlCommand sqlco = new SqlCommand();
            try
            {
                sqlco.Connection = objConn;

                sqlco.CommandText = SQLSTR;

                sqlread = sqlco.ExecuteReader();
                return sqlread;

            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLClass - GetDATAREADER");
                return null;
            }
            finally
            {
                sqlco.Dispose();
                //sqlread.Close()
            }
        }

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
                MessageBox.Show(ex.Message, "SQLClass - GetDATASET");
                return null;
            }
            finally
            {
                sqlco.Dispose();
                sqlAD.Dispose();
                sqlSET.Dispose();
            }
        }

        public SqlConnection GetConnection()
        {
            return objConn;
        }

        public object ExecuteSQLScalar(string SQLSTR)
        {
            SqlCommand sqlco = new SqlCommand();
            try
            {
                sqlco.Connection = objConn;
                sqlco.CommandText = SQLSTR;
                return sqlco.ExecuteScalar();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLClass - ExecuteSQLScalar");
                return "";
            }
            finally
            {
                sqlco.Dispose();
            }
        }

        public int ExecuteNonQuery(string SQLSTR)
        {
            int functionReturnValue = 0;
            SqlCommand sqlco = new SqlCommand();
            try
            {
                sqlco.Connection = objConn;
                sqlco.CommandText = SQLSTR;
                return sqlco.ExecuteNonQuery();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLClass - ExecuteSQL");
                functionReturnValue = 0;
            }
            finally
            {
                sqlco.Dispose();
            }
            return functionReturnValue;
        }

        public int ExecuteNonQuery(string SQLSTR, out SqlException ErrReport)
        {
            int functionReturnValue = 0;
            SqlCommand sqlco = new SqlCommand();
            ErrReport = null;

            try
            {

                sqlco.Connection = objConn;
                sqlco.CommandText = SQLSTR;

                return sqlco.ExecuteNonQuery();
            }
            catch (SqlException sEX)
            {
                ErrReport = sEX;
                functionReturnValue = 0;
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "SQLClass - ExecuteSQL");
                functionReturnValue = 0;
            }
            finally
            {
                sqlco.Dispose();
            }
            return functionReturnValue;
        }

        public void Close()
        {
            if ((objConn != null))
            {
                objConn.Close();
                objConn.Dispose();
            }
        }

        //public List<string> getTables()
        //{
        //    List<string> tbls = new List<string>();

        //    DataTable dT;

        //    dT = objConn.GetSchema("Tables");
        //    dT.DefaultView.Sort = "TABLE_NAME";

        //    foreach (DataRowView dR in dT.DefaultView)
        //    {

        //      //  if (dR["TABLE_TYPE"].ToString().ToLower() == "table")
        //            tbls.Add(dR["TABLE_NAME"].ToString());
        //    }

        //    dT.Dispose();

        //    return tbls;
        //}

    }

}
```

origin - http://www.pipiscrew.com/?p=3654 sqlite-bulk-insert-16000-rows-in-5seconds