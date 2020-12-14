---
title: o[xml] Select data by XML file as table in TSQL
author: PipisCrew
date: 2015-03-31
categories: []
toc: true
---

reference
[http://stackoverflow.com/a/7650105](http://stackoverflow.com/a/7650105)

at sql managment studio use :
```js
set @xmlData='<?xml version="1.0"?>
<arrayofspangemansfilter xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
<spangemansfilter>
<filterid>1219</filterid>
<name>Fred</name>
`510`
<department>N</department>
<number>305327</number>
</spangemansfilter>
<spangemansfilter>
<filterid>3578</filterid>
<name>Gary</name>
`001`
<department>B</department>
<number>0692690</number>
</spangemansfilter>
<spangemansfilter>
<filterid>3579</filterid>
<name>George</name>
`001`
<department>X</department>
<number>35933</number>
</spangemansfilter>
</arrayofspangemansfilter>'

SELECT 
  ref.value('FilterID[1]', 'int') AS FilterID ,
  ref.value('Name[1]', 'NVARCHAR (10)') AS Name ,
  ref.value('Code[1]', 'NVARCHAR (10)') AS Code ,
  ref.value('Department[1]', 'NVARCHAR (3)') AS Department,
  ref.value('Number[1]', 'int') AS Number      
FROM @xmlData.nodes('/ArrayOfSpangemansFilter/SpangemansFilter') 
xmlData( ref )
```

alternative solutions 
office 2013 > Ribbon-Tab 'Data' > Import from XML (took 5min to import 4mb XML)
http://blogs.msdn.com/b/simonince/archive/2009/04/24/flattening-xml-data-in-sql-server.aspx
http://www.databasejournal.com/features/mysql/importing-xml-csv-text-and-ms-excel-files-into-mysql.html

origin - http://www.pipiscrew.com/?p=2746 xml-select-data-by-xml-file-as-table-in-tsql