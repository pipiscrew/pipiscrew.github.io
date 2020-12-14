---
title: Convert Excel sheet to XML Elements or XML Attributes
author: PipisCrew
date: 2017-01-08
categories: [app]
toc: true
---

### *way1 - export as XML Elements*

0-Open the XLS file contain the data you want to export
If you try to File > Save as > XML Data you will get a messagebox :

> Cannot save XML data because the workbook does not contain any XML Mappings

1-Excel2010 > Go to Files > Options > Customize Ribbon, check the 'Developer', on the second list.  
    Excel2007 > Files > Options > Popular > Show Developer tab in Ribbon.
2-On the 'Developer' tab, there is a XML section, click the 'Source' button. A right bar will open, click the 'XML Maps' button. From here you can define the columns for your XML. You can import an existing XML (to get the structure) or a XSD. When using XML MUST contains 2records, otherwise cannot handle it.

```js
//sample of xml to get the structure/fields
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<row>
		<fullname>Brendan Merritt</fullname>
		<address>354 Lake View Drive Lake Mary</address>
		<tel>(430) 286-6649</tel>
	</row>
	<row>
		<fullname>Elisa Stokes</fullname>
		<address>538 Greenrose Street Muskego</address>
		<tel>(572) 343-7499</tel>
	</row> 
</root>
```

3-Import this^ will appear the structure of xml 
![pic1](https://www.pipiscrew.com/wp-content/uploads/2017/01/pic1.png)
4-Create a new sheet, from the right xml bar, drag the #root# element to A1 
![pic2](https://www.pipiscrew.com/wp-content/uploads/2017/01/pic2.png)
5-Copy&Paste the rows from your sheet to the new sheet that contains the XML columns, paste at row 2 (I dont know why is blue ask microsoft!)
6-File > Save as > XML Data

* * *

### *way 2 - using Microsoft AddIn to automate XML schema creation - export as XML Elements*

Guide -https://support.office.com/en-us/article/Create-an-XML-data-file-and-XML-schema-file-from-worksheet-data-e35400d4-0e10-4669-9a50-59a8c57d677e
or
http://franscribing.blogspot.gr/2013/05/how-to-convert-excel-2010-speadsheet-to.html
or
http://click-solutions.eu/IT-support/knowledgebase.php?article=1

1-Download the Excel 2003 XML Tools Add-in, and then follow the instructions.
2-Open Excel 2010, click on File > Options, select the Add-Ins category.
3-In the Manage box down at the bottom, click Go.
4-In the Add-Ins dialog box, click Browse, locate the XmlTools.xla file, select it and then click OK. By default, this file is stored in the following folder: C:\Office Samples\OfficeExcel2003XMLToolsAddin
5-Make sure the XmlTools check box is selected in the Add-Ins available list, and then click OK to load the add-in.
6-New Add-ins tab appear!
7-Open the XLS file contain the data you want to export, goto Add-ins tab > XML Tools > 'Convert a range to XML List'
8-click the 'Click here and drag select a range' > Select the range > Return back press enter to XML dialog > If the selection contains on first row the headers say to options
9-Click ok!

* * *

### *way 3  - export as XML Attributes*

The way1 + way2, export with XML Elements, using the following XML Mapping

```js
//source - http://stackoverflow.com/a/14724334
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<translations xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<item id="USER_NAME">
    <en>Username</en>
    <de>Username_D</de>
</item>
<item id="PASSWORD">
    <en>Password</en>
    <de>Password_D</de>
</item>
</translations>
```

you can produce XML attributes!! tested&working.

* * *

### *way 4  - using XSD (best way)*

the xsd template kept from bitwizards.com

```js
//original - https://bitwizards.com/Thought-Leadership/Blog/2010/November-2010/How-To-Export-an-Excel-2010-Worksheet-to-XML
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="NewsItemsTable">
        <xs:complextype>
            <xs:sequence>
                <xs:element ref="NewsItemRow" minoccurs="0" maxoccurs="unbounded"></xs:element>
            </xs:sequence>
        </xs:complextype>
    </xs:element>
    <xs:element name="NewsItemRow">
        <xs:complextype>
            <xs:sequence>
                <xs:element name="newstitle" type="xs:string"></xs:element>
                <xs:element name="newsdate" type="xs:dateTime"></xs:element>
                <xs:element name="newssummary" type="xs:string"></xs:element>
                <xs:element name="newstext" type="xs:string"></xs:element>
            </xs:sequence>
        </xs:complextype>
    </xs:element>
</xs:schema>
```

```js
//modded
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="NewsItemsTable">
        <xs:complextype>
            <xs:sequence>
                <xs:element ref="NewsItemRow" minoccurs="0" maxoccurs="unbounded"></xs:element>
            </xs:sequence>
        </xs:complextype>
    </xs:element>
    <xs:element name="NewsItemRow">
        <xs:complextype>
                <xs:attribute name="newstitle" type="xs:string"></xs:attribute>
                <xs:attribute name="newsdate" type="xs:dateTime"></xs:attribute>
                <xs:attribute name="newssummary" type="xs:string"></xs:attribute>
                <xs:attribute name="newstext" type="xs:string"></xs:attribute>
        </xs:complextype>
    </xs:element>
</xs:schema>
```

then having this in Excel 
![pic3](https://www.pipiscrew.com/wp-content/uploads/2017/01/pic3.png)

File > Save as > XML Data, finally EXCEL exports to attributes!!

```js
//here it is!
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<newsitemstable>
	<newsitemrow newstitle="iMagic" newsdate="2000-01-01T00:00:00.000" newssummary="010" newstext="RSS"></newsitemrow>
	<newsitemrow newstitle="decom" newsdate="2000-01-01T00:00:00.000" newssummary="010" newstext="RSS"></newsitemrow>
	<newsitemrow newstitle="DICOM" newsdate="2000-01-01T00:00:00.000" newssummary="010" newstext="ATOM"></newsitemrow>
	<newsitemrow newstitle="VueScan" newsdate="2000-01-01T00:00:00.000" newssummary="010" newstext="BBS"></newsitemrow>
	<newsitemrow newstitle="TNTsdk" newsdate="2000-01-01T00:00:00.000" newssummary="010" newstext="MAIL"></newsitemrow>
	<newsitemrow newstitle="YT Video" newsdate="2000-01-01T00:00:00.000" newssummary="010" newstext="IM"></newsitemrow>
</newsitemstable>
```

* * *

### *way 5  - misc*

convert elements to attributes via XLT
http://stackoverflow.com/a/6800505
http://www.shell-tools.net/index.php?op=xslt

XLS to XML Translate files between XLS / XLSX and XML format - http://xlstoxml.sourceforge.net/
Convert Excel Spreadsheet data to XML - www.youtube.com/watch?v=9bat12gH3Qs
Excel file to an XML data file, or vice versa - http://www.excel-easy.com/examples/xml.html
Exporting a Google Spreadsheet as JSON - http://blog.pamelafox.org/2013/06/exporting-google-spreadsheet-as-json.html or https://gist.github.com/pamelafox/1878143

software created - [XML Elements to Attributes](https://www.pipiscrew.com/works/xml-elements-to-attributes/)

#xml #attributes #elements #excel #sheet

origin - http://www.pipiscrew.com/?p=6399 convert-excel-sheet-to-xml-elements-or-xml-attributes