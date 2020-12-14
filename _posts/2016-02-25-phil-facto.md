---
title: Phil Factor - parseJSON function
author: PipisCrew
date: 2016-02-25
categories: [sql]
toc: true
---

microsoft.Mai Trọng Khánh  writes :

> The first question: Why do you need to parse JSON by SQL script? You can do it easily by C# or VB, or any PL.
> But I sure that if you search this keyword and reach this post, you already have your own reason.
> In my case, I got a task from Chris (my manager) in Microsoft, he want to migrate database, one of those step is parse about 100 k Json string and Insert into new table.
> I have tried with C#, it worked, but I don't know how long, because I recognize that it is not a smart way and stop them ( program is running and thinking about C# solution). I try with SQL script.

continue reading - [http://mtkcode.blogspot.gr/2014/08/parse-json-string-by-sql-script.html](http://mtkcode.blogspot.gr/2014/08/parse-json-string-by-sql-script.html)
the script to dropbox - [https://www.dropbox.com/s/7ka7fbjt400i31k/ParseJSON-FUNCTION.sql](https://www.dropbox.com/s/7ka7fbjt400i31k/ParseJSON-FUNCTION.sql)

### Original Developer - Phil Factor - blog article

[https://www.simple-talk.com/sql/t-sql-programming/consuming-json-strings-in-sql-server/](https://www.simple-talk.com/sql/t-sql-programming/consuming-json-strings-in-sql-server/)

at line 51 maybe is useful to make these replacements :
```js
  Set @JSON = REPLACE(@JSON, '[', '')
  Set @JSON = REPLACE(@JSON, ']', '')
  Set @JSON = REPLACE(@JSON, CHAR(9), '')
  Set @JSON = REPLACE(@JSON, CHAR(13), '')
  Set @JSON = REPLACE(@JSON, CHAR(10), '')
```

so we have :

```js

CREATE FUNCTION [dbo].[parseJSON]( @JSON NVARCHAR(MAX))
/*
-- Create by Phil Factor	15 November 2010
-- Update by Kaden Mai		21 August 2014
-- How to Use	http://mtkcode.blogspot.com/2014/08/parse-json-string-by-sql-script.html
*/
RETURNS @hierarchy TABLE
  (
   element_id INT IDENTITY(1, 1) NOT NULL, /* internal surrogate primary key gives the order of parsing and the list order */
   sequenceNo [int] NULL, /* the place in the sequence for the element */
   parent_ID INT,/* if the element has a parent then it is in this column. The document is the ultimate parent, so you can get the structure from recursing from the document */
   Object_ID INT,/* each list or object has an object id. This ties all elements to a parent. Lists are treated as objects here */
   NAME NVARCHAR(2000),/* the name of the object */
   StringValue NVARCHAR(MAX) NOT NULL,/*the string representation of the value of the element. */
   ValueType VARCHAR(10) NOT null /* the declared type of the value represented as a string in StringValue*/
  )
AS
BEGIN
  DECLARE
    @FirstObject INT, --the index of the first open bracket found in the JSON string
    @OpenDelimiter INT,--the index of the next open bracket found in the JSON string
    @NextOpenDelimiter INT,--the index of subsequent open bracket found in the JSON string
    @NextCloseDelimiter INT,--the index of subsequent close bracket found in the JSON string
    @Type NVARCHAR(10),--whether it denotes an object or an array
    @NextCloseDelimiterChar CHAR(1),--either a '}' or a ']'
    @Contents NVARCHAR(MAX), --the unparsed contents of the bracketed expression
    @Start INT, --index of the start of the token that you are parsing
    @end INT,--index of the end of the token that you are parsing
    @param INT,--the parameter at the end of the next Object/Array token
    @EndOfName INT,--the index of the start of the parameter at end of Object/Array token
    @token NVARCHAR(200),--either a string or object
    @value NVARCHAR(MAX), -- the value as a string
    @SequenceNo int, -- the sequence number within a list
    @name NVARCHAR(200), --the name as a string
    @parent_ID INT,--the next parent ID to allocate
    @lenJSON INT,--the current length of the JSON String
    @characters NCHAR(36),--used to convert hex to decimal
    @result BIGINT,--the value of the hex symbol being parsed
    @index SMALLINT,--used for parsing the hex value
    @Escape INT --the index of the next escape character

  DECLARE @Strings TABLE /* in this temporary table we keep all strings, even the names of the elements, since they are 'escaped' in a different way, and may contain, unescaped, brackets denoting objects or lists. These are replaced in the JSON string by tokens representing the string */
    (
     String_ID INT IDENTITY(1, 1),
     StringValue NVARCHAR(MAX)
    )

  --replacements
  Set @JSON = REPLACE(@JSON, '[', '')
  Set @JSON = REPLACE(@JSON, ']', '')
  Set @JSON = REPLACE(@JSON, CHAR(9), '')
  Set @JSON = REPLACE(@JSON, CHAR(13), '')
  Set @JSON = REPLACE(@JSON, CHAR(10), '')

  SELECT--initialise the characters to convert hex to ascii
    @characters='0123456789abcdefghijklmnopqrstuvwxyz',
    @SequenceNo=0, --set the sequence no. to something sensible.
  /* firstly we process all strings. This is done because [{} and ] aren't escaped in strings, which complicates an iterative parse. */
    @parent_ID=0;
  WHILE 1=1 --forever until there is nothing more to do
    BEGIN
      SELECT
        @start=PATINDEX('%[^a-zA-Z]["]%', @json collate SQL_Latin1_General_CP850_Bin);--next delimited string
      IF @start=0 BREAK --no more so drop through the WHILE loop
      IF SUBSTRING(@json, @start+1, 1)='"'
        BEGIN --Delimited Name
          SET @start=@Start+1;
          SET @end=PATINDEX('%[^\]["]%', RIGHT(@json, LEN(@json+'|')-@start) collate SQL_Latin1_General_CP850_Bin);
        END
      IF @end=0 --no end delimiter to last string
        BREAK --no more
      SELECT @token=SUBSTRING(@json, @start+1, @end-1)
      --now put in the escaped control characters
      SELECT @token=REPLACE(@token, FROMString, TOString)
      FROM
        (SELECT
          '\"' AS FromString, '"' AS ToString
         UNION ALL SELECT '\\', '\'
         UNION ALL SELECT '\/', '/'
         UNION ALL SELECT '\b', CHAR(08)
         UNION ALL SELECT '\f', CHAR(12)
         UNION ALL SELECT '\n', CHAR(10)
         UNION ALL SELECT '\r', CHAR(13)
         UNION ALL SELECT '\t', CHAR(09)
        ) substitutions
      SELECT @result=0, @escape=1
  --Begin to take out any hex escape codes
      WHILE @escape>0
        BEGIN
          SELECT @index=0,
          --find the next hex escape sequence
          @escape=PATINDEX('%\x[0-9a-f][0-9a-f][0-9a-f][0-9a-f]%', @token collate SQL_Latin1_General_CP850_Bin)
          IF @escape>0 --if there is one
            BEGIN
              WHILE @index<4 --there="" are="" always="" four="" digits="" to="" a="" \x="" sequence="" begin="" select="" --determine="" its="" value="" @result="@result+POWER(16," @index)="" *(charindex(substring(@token,="" @escape+2+3-@index,="" 1),="" @characters)-1),="" @index="@index+1" ;="" end="" --="" and="" replace="" the="" hex="" sequence="" by="" its="" unicode="" value="" select="" @token="STUFF(@token," @escape,="" 6,="" nchar(@result))="" end="" end="" --now="" store="" the="" string="" away="" insert="" into="" @strings="" (stringvalue)="" select="" @token="" --="" and="" replace="" the="" string="" with="" a="" token="" select="" @json="STUFF(@json," @start,="" @end+1,="" '@string'+convert(nvarchar(5),="" @@identity))="" end="" --="" all="" strings="" are="" now="" removed.="" now="" we="" find="" the="" first="" leaf.="" while="" 1="1" --forever="" until="" there="" is="" nothing="" more="" to="" do="" begin="" select="" @parent_id="@parent_ID+1" --find="" the="" first="" object="" or="" list="" by="" looking="" for="" the="" open="" bracket="" select="" @firstobject="PATINDEX('%[{[[]%'," @json="" collate="" sql_latin1_general_cp850_bin)--object="" or="" array="" if="" @firstobject="0" break="" if="" (substring(@json,="" @firstobject,="" 1)='{' )="" select="" @nextclosedelimiterchar='}' ,="" @type='object' else="" select="" @nextclosedelimiterchar=']' ,="" @type='array' select="" @opendelimiter="@firstObject" while="" 1="1" --find="" the="" innermost="" object="" or="" list...="" begin="" select="" @lenjson="LEN(@JSON+'|')-1" --find="" the="" matching="" close-delimiter="" proceeding="" after="" the="" open-delimiter="" select="" @nextclosedelimiter="CHARINDEX(@NextCloseDelimiterChar," @json,="" @opendelimiter+1)="" --is="" there="" an="" intervening="" open-delimiter="" of="" either="" type="" select="" @nextopendelimiter="PATINDEX('%[{[[]%'," right(@json,="" @lenjson-@opendelimiter)collate="" sql_latin1_general_cp850_bin)--object="" if="" @nextopendelimiter="0" break="" select="" @nextopendelimiter="@NextOpenDelimiter+@OpenDelimiter" if=""></4><@nextopendelimiter break="" if="" substring(@json,="" @nextopendelimiter,="" 1)='{' select="" @nextclosedelimiterchar='}' ,="" @type='object' else="" select="" @nextclosedelimiterchar=']' ,="" @type='array' select="" @opendelimiter="@NextOpenDelimiter" end="" ---and="" parse="" out="" the="" list="" or="" name/value="" pairs="" select="" @contents="SUBSTRING(@json," @opendelimiter+1,="" @nextclosedelimiter-@opendelimiter-1)="" select="" @json="STUFF(@json," @opendelimiter,="" @nextclosedelimiter-@opendelimiter+1,="" '@'+@type+convert(nvarchar(5),="" @parent_id))="" while="" (patindex('%[a-za-z0-9@+.e]%',="" @contents="" collate=""></@nextopendelimiter><>0
    BEGIN
      IF @Type='Object' --it will be a 0-n list containing a string followed by a string, number,boolean, or null
        BEGIN
          SELECT
            @SequenceNo=0,@end=CHARINDEX(':', ' '+@contents)--if there is anything, it will be a string-based name.
          SELECT  @start=PATINDEX('%[^A-Za-z@][@]%', ' '+@contents collate SQL_Latin1_General_CP850_Bin)--AAAAAAAA
          SELECT @token=SUBSTRING(' '+@contents, @start+1, @End-@Start-1),
            @endofname=PATINDEX('%[0-9]%', @token collate SQL_Latin1_General_CP850_Bin),
            @param=RIGHT(@token, LEN(@token)-@endofname+1)
          SELECT
            @token=LEFT(@token, @endofname-1),
            @Contents=RIGHT(' '+@contents, LEN(' '+@contents+'|')-@end-1)
          SELECT  @name=stringvalue FROM @strings
            WHERE string_id=@param --fetch the name
        END
      ELSE
        SELECT @Name=null,@SequenceNo=@SequenceNo+1
      SELECT
        @end=CHARINDEX(',', @contents)-- a string-token, object-token, list-token, number,boolean, or null
      IF @end=0
        SELECT  @end=PATINDEX('%[A-Za-z0-9@+.e][^A-Za-z0-9@+.e]%', @Contents+' ' collate SQL_Latin1_General_CP850_Bin)
          +1
       SELECT
         @start=PATINDEX('%[^A-Za-z0-9@+.e][A-Za-z0-9@+.e][\-]%', ' '+@contents collate SQL_Latin1_General_CP850_Bin)
		-- Edited: add more condition [\-] in order to detect negative number 08-20-2014
      --select @start,@end, LEN(@contents+'|'), @contents 
      SELECT
        @Value=RTRIM(SUBSTRING(@contents, @start, @End-@Start)),
        @Contents=RIGHT(@contents+' ', LEN(@contents+'|')-@end)
      IF SUBSTRING(@value, 1, 7)='@object'
        INSERT INTO @hierarchy
          (NAME, SequenceNo, parent_ID, StringValue, Object_ID, ValueType)
          SELECT @name, @SequenceNo, @parent_ID, SUBSTRING(@value, 8, 5),
            SUBSTRING(@value, 8, 5), 'object'
      ELSE
        IF SUBSTRING(@value, 1, 6)='@array'
          INSERT INTO @hierarchy
            (NAME, SequenceNo, parent_ID, StringValue, Object_ID, ValueType)
            SELECT @name, @SequenceNo, @parent_ID, SUBSTRING(@value, 7, 5),
              SUBSTRING(@value, 7, 5), 'array'
        ELSE
          IF SUBSTRING(@value, 1, 7)='@string'
            INSERT INTO @hierarchy
              (NAME, SequenceNo, parent_ID, StringValue, ValueType)
              SELECT @name, @SequenceNo, @parent_ID, stringvalue, 'string'
              FROM @strings
              WHERE string_id=SUBSTRING(@value, 8, 5)
          ELSE
            IF @value IN ('true', 'false')
              INSERT INTO @hierarchy
                (NAME, SequenceNo, parent_ID, StringValue, ValueType)
                SELECT @name, @SequenceNo, @parent_ID, @value, 'boolean'
            ELSE
              IF @value='null'
                INSERT INTO @hierarchy
                  (NAME, SequenceNo, parent_ID, StringValue, ValueType)
                  SELECT @name, @SequenceNo, @parent_ID, @value, 'null'
              ELSE
                IF PATINDEX('%[^0-9]%', @value collate SQL_Latin1_General_CP850_Bin)>0
                  INSERT INTO @hierarchy
                    (NAME, SequenceNo, parent_ID, StringValue, ValueType)
                    SELECT @name, @SequenceNo, @parent_ID, @value, 'real'
                ELSE
                  INSERT INTO @hierarchy
                    (NAME, SequenceNo, parent_ID, StringValue, ValueType)
                    SELECT @name, @SequenceNo, @parent_ID, @value, 'int'
      if @Contents=' ' Select @SequenceNo=0
    END
  END
INSERT INTO @hierarchy (NAME, SequenceNo, parent_ID, StringValue, Object_ID, ValueType)
  SELECT '-',1, NULL, '', @parent_id-1, @type
--
   RETURN
END

```

## example of call 

```js
select * from 
ParseJSON ('{
   "time": "11:46:21 AM",
   "milliseconds_since_epoch": 1456400781421,
   "date": "02-25-2016"
}')
```

## example of temporary table use

```js
--if temporary table exists drop it
IF object_id('tempdb..#RESULTSET') IS NOT NULL
BEGIN
	DROP TABLE #RESULTSET
END

--create temporary table
CREATE TABLE #RESULTSET (
	NAME NVARCHAR(255)
	,txt NVARCHAR(255)
);

--insert to temporary table
INSERT INTO [#RESULTSET]
SELECT NAME
	,StringValue
FROM ParseJSON('{"name":"$test1","typee":"button","caption":"MainMenu","author":"PipisCrew"},{"name":"$test2","typee":"checkbox","caption":"Online","author":"PipisCrew}')

--select by temporary table
SELECT *
FROM #RESULTSET
```

## example of table use

![snap184](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap184.png)

```js
--insert to temporary table
INSERT INTO [a_test]
SELECT NAME
	,StringValue
FROM ParseJSON('{"name":"$test1","typee":"button","caption":"MainMenu","author":"PipisCrew"},{"name":"$test2","typee":"checkbox","caption":"Online","author":"PipisCrew}')

--select by temporary table
SELECT *
FROM [a_test]
```

![snap185](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap185.png)

origin - http://www.pipiscrew.com/?p=3197 sql-phil-factor-parsejson-function