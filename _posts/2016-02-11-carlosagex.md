---
title: CarlosAg.ExcelXmlWriter
author: PipisCrew
date: 2016-02-11
categories: [.net]
toc: true
---

homepage - [http://www.carlosag.net/Tools/ExcelXmlWriter/](http://www.carlosag.net/Tools/ExcelXmlWriter/)

basic example by CarlosAg.ExcelXmlWriter homepage
```js
using CarlosAg.ExcelXmlWriter;

class TestApp {
    static void Main(string[] args) {
        Workbook book = new Workbook();
        Worksheet sheet = book.Worksheets.Add("Sample");
        WorksheetRow row =  sheet.Table.Rows.Add();
        row.Cells.Add("Hello World");
        book.Save(@"c:\test.xls");
    }
}
```

what about export a datatable to xls ?

```js
DataTable dataTable = conn.GetDATATABLE("select * from products order by categorycaption_title,product_code");

	Workbook book = new Workbook();
	ExcelDataTableWriter edtw = new ExcelDataTableWriter();

	Worksheet sheet = book.Worksheets.Add("Export" + DateTime.Now.ToString("yyyyMMdd"));
	edtw.PopulateWorksheet(dataTable, sheet);

	//WorksheetRow row = sheet.Table.Rows.Add();
	//row.Cells.Add("Hello World");
	string fl;
	fl = Application.StartupPath + "\\export" + DateTime.Now.ToString("yyyyMMdd") + ".xls";
	book.Save(fl);

	MessageBox.Show(Application.StartupPath + "\\" + fl + " \r\n\r\nCreated with success!", Application.ProductName, MessageBoxButtons.OK, MessageBoxIcon.Information);
```

```js
//source - http://www.sitepoint.com/making-excel-the-carlosag-way/
//author - Wyatt Barnett
//date   - August 22, 2006

using System.Data;
using CarlosAg.ExcelXmlWriter;
using System;

namespace WWB.ExcelDatasetWriter
{
    /// <summary>
    /// Writes a datatable to a worksheet using the CarlosAG.ExcelXmlWriter library.
    /// </summary>

    public class ExcelDataTableWriter
    {
        public ExcelDataTableWriter()
        { }

        public void PopulateWorksheet(DataTable dt, Worksheet toPopulate)
        {
            PopulateWorksheet(dt, toPopulate, true);
        }

        public void PopulateWorksheet(DataTable dt, Worksheet toPopulate, bool makeHeader)
        {
            //check valid input
            if (toPopulate == null)
            {
                throw new ArgumentNullException("toPopulate", "Worksheet cannot be null.");
            }
            if (dt == null)
            {
                throw new ArgumentNullException("dt", "DataTable cannot be null");
            }
            //Parse the columns
            ColumnType[] colDesc = parseColumns(dt);
            //Create header row
            if (makeHeader)
            {
                toPopulate.Table.Rows.Insert(0, makeHeaderRow(colDesc));
            }
            //Create rows
            foreach (DataRow row in dt.Rows)
            {
                toPopulate.Table.Rows.Add(makeDataRow(colDesc, row));
            }
        }

        #region row + cell making

        private WorksheetRow makeHeaderRow(ColumnType[] cols)
        {
            WorksheetRow ret = new WorksheetRow();
            foreach (ColumnType ctd in cols)
            {
                ret.Cells.Add(ctd.GetHeaderCell());
            }
            return ret;
        }

        private WorksheetRow makeDataRow(ColumnType[] ctds, DataRow row)
        {
            WorksheetRow ret = new WorksheetRow();
            WorksheetCell tmp = null;
            for (int i = 0; i < row.table.columns.count;="" i++)="" {="" tmp="ctds[i].GetDataCell(row[i]);" ret.cells.add(tmp);="" }="" return="" ret;="" }="" #endregion="" #region="" column="" parsing="" private="" columntype[]="" parsecolumns(datatable="" dt)="" {="" columntype[]="" ret="new" columntype[dt.columns.count];="" columntype="" ctd="null;" for="" (int="" i="0;" i="">< dt.columns.count;="" i++)="" {="" ctd="new" columntype();="" ctd.name="dt.Columns[i].ColumnName;" getdatatype(dt.columns[i],="" ctd);="" ret[i]="ctd;" }="" return="" ret;="" }="" private="" void="" getdatatype(datacolumn="" col,="" columntype="" desc)="" {="" if="" (col.datatype="=" typeof(datetime))="" {="" desc.exceltype="DataType.DateTime;" }="" else="" if="" (col.datatype="=" typeof(string))="" {="" desc.exceltype="DataType.String;" }="" else="" if="" (col.datatype="=" typeof(sbyte)="" ||="" col.datatype="=" typeof(byte)="" ||="" col.datatype="=" typeof(short)="" ||="" col.datatype="=" typeof(ushort)="" ||="" col.datatype="=" typeof(int)="" ||="" col.datatype="=" typeof(uint)="" ||="" col.datatype="=" typeof(long)="" ||="" col.datatype="=" typeof(ulong)="" ||="" col.datatype="=" typeof(float)="" ||="" col.datatype="=" typeof(double)="" ||="" col.datatype="=" typeof(decimal)="" )="" {="" desc.exceltype="DataType.Number;" }="" else="" {="" desc.exceltype="DataType.String;" }="" }="" #endregion="" }=""><summary>
    /// Creates an excel-friendly Xml Document from a dataset using the CarlosAg.ExcelXmlWriter library.
    /// </summary>

    public class ExcelDatasetWriter
    {
        public ExcelDatasetWriter()
        { }

        public Workbook CreateWorkbook(DataSet data)
        {
            //ensure valid data
            if (data == null)
            {
                throw new ArgumentNullException("data", "Data cannot be null.");
            }
            ensureTables(data);

            //Variable declarations
            //our workbook
            Workbook wb = new Workbook();
            //Our worksheet container
            Worksheet ws;
            //Our DataTableWriter
            ExcelDataTableWriter edtw = new ExcelDataTableWriter();
            //Our sheet name
            string wsName;
            //Our counter
            int tCnt = 0;

            //Loop through datatables and create worksheets
            foreach (DataTable dt in data.Tables)
            {
                //set the name of the worksheet
                if (dt.TableName != null && dt.TableName.Length > 0 && dt.TableName != "Table")
                {
                    wsName = dt.TableName;
                }
                else
                {
                    //Go to generic Sheet1 . . . SheetN
                    wsName = "Sheet" + (tCnt + 1).ToString();
                }
                //Instantiate the worksheet
                ws = wb.Worksheets.Add(wsName);
                //Populate the worksheet
                edtw.PopulateWorksheet(dt, ws);
                tCnt++;
            }
            return wb;
        }

        private void ensureTables(DataSet data)
        {
            if (data.Tables.Count == 0)
            {
                throw new ArgumentOutOfRangeException("data", "DataSet does not contain any tables.");
            }
        }
    }

    /// <summary>
    /// Creates a Column for CarlosAg.ExcelXmlWriter
    /// </summary>

    internal class ColumnType
    {
        public ColumnType()
        { }
        private string name;
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        private DataType excelType;
        public DataType ExcelType
        {
            get { return excelType; }
            set { excelType = value; }
        }

        public WorksheetCell GetHeaderCell()
        {
            WorksheetCell head = new WorksheetCell(Name, DataType.String);
            return head;
        }

        private string getDataTypeFormatString()
        {
            if (ExcelType == DataType.DateTime)
            {
                return "s";
            }
            return null;
        }

        public WorksheetCell GetDataCell(object data)
        {
            WorksheetCell dc = new WorksheetCell();
            dc.Data.Type = ExcelType;
            if (ExcelType == DataType.DateTime && data is DateTime)
            {
                DateTime dt = (DateTime)data;
                dc.Data.Text = dt.ToString("s");
            }
            else
            {
                string dataString = data.ToString();
                if (dataString == null || dataString.Length == 0)
                {
                    dc.Data.Type = DataType.String;
                    dc.Data.Text = string.Empty;
                }
                else
                {
                    dc.Data.Text = dataString;
                }
            }
            return dc;
        }
    }
}
```

origin - http://www.pipiscrew.com/?p=3717 net-carlosag-excelxmlwriter