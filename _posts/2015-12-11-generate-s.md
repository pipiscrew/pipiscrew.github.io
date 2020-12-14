---
title: generate scripts + alternative
author: PipisCrew
date: 2015-12-11
categories: [sql]
toc: true
---

[http://stackoverflow.com/a/1515975](http://stackoverflow.com/a/1515975)
In SSMS in the Object Explorer, right click on the database right-click and pick "Tasks" and then "Generate Scripts".

* * *

### Method 1

For example, it lets you do this: To generate INSERT statements for table 'titles':

```js
//http://stackoverflow.com/a/982587
EXEC sp_generate_inserts 'titles'
```

```js
--source :
--http://vyaskn.tripod.com/code.htm#inserts
--http://vyaskn.tripod.com/code/generate_inserts_2005.txt
SET NOCOUNT ON
GO

PRINT 'Using Master database'
USE master
GO

PRINT 'Checking for the existence of this procedure'
IF (SELECT OBJECT_ID('sp_generate_inserts','P')) IS NOT NULL --means, the procedure already exists
	BEGIN
		PRINT 'Procedure already exists. So, dropping it'
		DROP PROC sp_generate_inserts
	END
GO

CREATE PROC sp_generate_inserts
(
	@table_name varchar(776),  		-- The table/view for which the INSERT statements will be generated using the existing data
	@target_table varchar(776) = NULL, 	-- Use this parameter to specify a different table name into which the data will be inserted
	@include_column_list bit = 1,		-- Use this parameter to include/ommit column list in the generated INSERT statement
	@from varchar(800) = NULL, 		-- Use this parameter to filter the rows based on a filter condition (using WHERE)
	@include_timestamp bit = 0, 		-- Specify 1 for this parameter, if you want to include the TIMESTAMP/ROWVERSION column's data in the INSERT statement
	@debug_mode bit = 0,			-- If @debug_mode is set to 1, the SQL statements constructed by this procedure will be printed for later examination
	@owner varchar(64) = NULL,		-- Use this parameter if you are not the owner of the table
	@ommit_images bit = 0,			-- Use this parameter to generate INSERT statements by omitting the 'image' columns
	@ommit_identity bit = 0,		-- Use this parameter to ommit the identity columns
	@top int = NULL,			-- Use this parameter to generate INSERT statements only for the TOP n rows
	@cols_to_include varchar(8000) = NULL,	-- List of columns to be included in the INSERT statement
	@cols_to_exclude varchar(8000) = NULL,	-- List of columns to be excluded from the INSERT statement
	@disable_constraints bit = 0,		-- When 1, disables foreign key constraints and enables them after the INSERT statements
	@ommit_computed_cols bit = 0		-- When 1, computed columns will not be included in the INSERT statement

)
AS
BEGIN

/***********************************************************************************************************
Procedure:	sp_generate_inserts  (Build 22) 
		(Copyright © 2002 Narayana Vyas Kondreddi. All rights reserved.)

Purpose:	To generate INSERT statements from existing data. 
		These INSERTS can be executed to regenerate the data at some other location.
		This procedure is also useful to create a database setup, where in you can 
		script your data along with your table definitions.

Written by:	Narayana Vyas Kondreddi
	        http://vyaskn.tripod.com

Acknowledgements:
		Divya Kalra	-- For beta testing
		Mark Charsley	-- For reporting a problem with scripting uniqueidentifier columns with NULL values
		Artur Zeygman	-- For helping me simplify a bit of code for handling non-dbo owned tables
		Joris Laperre   -- For reporting a regression bug in handling text/ntext columns

Tested on: 	SQL Server 7.0 and SQL Server 2000 and SQL Server 2005

Date created:	January 17th 2001 21:52 GMT

Date modified:	May 1st 2002 19:50 GMT

Email: 		vyaskn@hotmail.com

NOTE:		This procedure may not work with tables with too many columns.
		Results can be unpredictable with huge text columns or SQL Server 2000's sql_variant data types
		Whenever possible, Use @include_column_list parameter to ommit column list in the INSERT statement, for better results
		IMPORTANT: This procedure is not tested with internation data (Extended characters or Unicode). If needed
		you might want to convert the datatypes of character variables in this procedure to their respective unicode counterparts
		like nchar and nvarchar

		ALSO NOTE THAT THIS PROCEDURE IS NOT UPDATED TO WORK WITH NEW DATA TYPES INTRODUCED IN SQL SERVER 2005 / YUKON

Example 1:	To generate INSERT statements for table 'titles':

		EXEC sp_generate_inserts 'titles'

Example 2: 	To ommit the column list in the INSERT statement: (Column list is included by default)
		IMPORTANT: If you have too many columns, you are advised to ommit column list, as shown below,
		to avoid erroneous results

		EXEC sp_generate_inserts 'titles', @include_column_list = 0

Example 3:	To generate INSERT statements for 'titlesCopy' table from 'titles' table:

		EXEC sp_generate_inserts 'titles', 'titlesCopy'

Example 4:	To generate INSERT statements for 'titles' table for only those titles 
		which contain the word 'Computer' in them:
		NOTE: Do not complicate the FROM or WHERE clause here. It's assumed that you are good with T-SQL if you are using this parameter

		EXEC sp_generate_inserts 'titles', @from = "from titles where title like '%Computer%'"

Example 5: 	To specify that you want to include TIMESTAMP column's data as well in the INSERT statement:
		(By default TIMESTAMP column's data is not scripted)

		EXEC sp_generate_inserts 'titles', @include_timestamp = 1

Example 6:	To print the debug information:

		EXEC sp_generate_inserts 'titles', @debug_mode = 1

Example 7: 	If you are not the owner of the table, use @owner parameter to specify the owner name
		To use this option, you must have SELECT permissions on that table

		EXEC sp_generate_inserts Nickstable, @owner = 'Nick'

Example 8: 	To generate INSERT statements for the rest of the columns excluding images
		When using this otion, DO NOT set @include_column_list parameter to 0.

		EXEC sp_generate_inserts imgtable, @ommit_images = 1

Example 9: 	To generate INSERT statements excluding (ommiting) IDENTITY columns:
		(By default IDENTITY columns are included in the INSERT statement)

		EXEC sp_generate_inserts mytable, @ommit_identity = 1

Example 10: 	To generate INSERT statements for the TOP 10 rows in the table:

		EXEC sp_generate_inserts mytable, @top = 10

Example 11: 	To generate INSERT statements with only those columns you want:

		EXEC sp_generate_inserts titles, @cols_to_include = "'title','title_id','au_id'"

Example 12: 	To generate INSERT statements by omitting certain columns:

		EXEC sp_generate_inserts titles, @cols_to_exclude = "'title','title_id','au_id'"

Example 13:	To avoid checking the foreign key constraints while loading data with INSERT statements:

		EXEC sp_generate_inserts titles, @disable_constraints = 1

Example 14: 	To exclude computed columns from the INSERT statement:
		EXEC sp_generate_inserts MyTable, @ommit_computed_cols = 1
***********************************************************************************************************/

SET NOCOUNT ON

--Making sure user only uses either @cols_to_include or @cols_to_exclude
IF ((@cols_to_include IS NOT NULL) AND (@cols_to_exclude IS NOT NULL))
	BEGIN
		RAISERROR('Use either @cols_to_include or @cols_to_exclude. Do not use both the parameters at once',16,1)
		RETURN -1 --Failure. Reason: Both @cols_to_include and @cols_to_exclude parameters are specified
	END

--Making sure the @cols_to_include and @cols_to_exclude parameters are receiving values in proper format
IF ((@cols_to_include IS NOT NULL) AND (PATINDEX('''%''',@cols_to_include) = 0))
	BEGIN
		RAISERROR('Invalid use of @cols_to_include property',16,1)
		PRINT 'Specify column names surrounded by single quotes and separated by commas'
		PRINT 'Eg: EXEC sp_generate_inserts titles, @cols_to_include = "''title_id'',''title''"'
		RETURN -1 --Failure. Reason: Invalid use of @cols_to_include property
	END

IF ((@cols_to_exclude IS NOT NULL) AND (PATINDEX('''%''',@cols_to_exclude) = 0))
	BEGIN
		RAISERROR('Invalid use of @cols_to_exclude property',16,1)
		PRINT 'Specify column names surrounded by single quotes and separated by commas'
		PRINT 'Eg: EXEC sp_generate_inserts titles, @cols_to_exclude = "''title_id'',''title''"'
		RETURN -1 --Failure. Reason: Invalid use of @cols_to_exclude property
	END

--Checking to see if the database name is specified along wih the table name
--Your database context should be local to the table for which you want to generate INSERT statements
--specifying the database name is not allowed
IF (PARSENAME(@table_name,3)) IS NOT NULL
	BEGIN
		RAISERROR('Do not specify the database name. Be in the required database and just specify the table name.',16,1)
		RETURN -1 --Failure. Reason: Database name is specified along with the table name, which is not allowed
	END

--Checking for the existence of 'user table' or 'view'
--This procedure is not written to work on system tables
--To script the data in system tables, just create a view on the system tables and script the view instead

IF @owner IS NULL
	BEGIN
		IF ((OBJECT_ID(@table_name,'U') IS NULL) AND (OBJECT_ID(@table_name,'V') IS NULL)) 
			BEGIN
				RAISERROR('User table or view not found.',16,1)
				PRINT 'You may see this error, if you are not the owner of this table or view. In that case use @owner parameter to specify the owner name.'
				PRINT 'Make sure you have SELECT permission on that table or view.'
				RETURN -1 --Failure. Reason: There is no user table or view with this name
			END
	END
ELSE
	BEGIN
		IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = @table_name AND (TABLE_TYPE = 'BASE TABLE' OR TABLE_TYPE = 'VIEW') AND TABLE_SCHEMA = @owner)
			BEGIN
				RAISERROR('User table or view not found.',16,1)
				PRINT 'You may see this error, if you are not the owner of this table. In that case use @owner parameter to specify the owner name.'
				PRINT 'Make sure you have SELECT permission on that table or view.'
				RETURN -1 --Failure. Reason: There is no user table or view with this name		
			END
	END

--Variable declarations
DECLARE		@Column_ID int, 		
		@Column_List varchar(8000), 
		@Column_Name varchar(128), 
		@Start_Insert varchar(786), 
		@Data_Type varchar(128), 
		@Actual_Values varchar(8000),	--This is the string that will be finally executed to generate INSERT statements
		@IDN varchar(128)		--Will contain the IDENTITY column's name in the table

--Variable Initialization
SET @IDN = ''
SET @Column_ID = 0
SET @Column_Name = ''
SET @Column_List = ''
SET @Actual_Values = ''

IF @owner IS NULL 
	BEGIN
		SET @Start_Insert = 'INSERT INTO ' + '[' + RTRIM(COALESCE(@target_table,@table_name)) + ']' 
	END
ELSE
	BEGIN
		SET @Start_Insert = 'INSERT ' + '[' + LTRIM(RTRIM(@owner)) + '].' + '[' + RTRIM(COALESCE(@target_table,@table_name)) + ']' 		
	END

--To get the first column's ID

SELECT	@Column_ID = MIN(ORDINAL_POSITION) 	
FROM	INFORMATION_SCHEMA.COLUMNS (NOLOCK) 
WHERE 	TABLE_NAME = @table_name AND
(@owner IS NULL OR TABLE_SCHEMA = @owner)

--Loop through all the columns of the table, to get the column names and their data types
WHILE @Column_ID IS NOT NULL
	BEGIN
		SELECT 	@Column_Name = QUOTENAME(COLUMN_NAME), 
		@Data_Type = DATA_TYPE 
		FROM 	INFORMATION_SCHEMA.COLUMNS (NOLOCK) 
		WHERE 	ORDINAL_POSITION = @Column_ID AND 
		TABLE_NAME = @table_name AND
		(@owner IS NULL OR TABLE_SCHEMA = @owner)

		IF @cols_to_include IS NOT NULL --Selecting only user specified columns
		BEGIN
			IF CHARINDEX( '''' + SUBSTRING(@Column_Name,2,LEN(@Column_Name)-2) + '''',@cols_to_include) = 0 
			BEGIN
				GOTO SKIP_LOOP
			END
		END

		IF @cols_to_exclude IS NOT NULL --Selecting only user specified columns
		BEGIN
			IF CHARINDEX( '''' + SUBSTRING(@Column_Name,2,LEN(@Column_Name)-2) + '''',@cols_to_exclude) <> 0 
			BEGIN
				GOTO SKIP_LOOP
			END
		END

		--Making sure to output SET IDENTITY_INSERT ON/OFF in case the table has an IDENTITY column
		IF (SELECT COLUMNPROPERTY( OBJECT_ID(QUOTENAME(COALESCE(@owner,USER_NAME())) + '.' + @table_name),SUBSTRING(@Column_Name,2,LEN(@Column_Name) - 2),'IsIdentity')) = 1 
		BEGIN
			IF @ommit_identity = 0 --Determing whether to include or exclude the IDENTITY column
				SET @IDN = @Column_Name
			ELSE
				GOTO SKIP_LOOP			
		END

		--Making sure whether to output computed columns or not
		IF @ommit_computed_cols = 1
		BEGIN
			IF (SELECT COLUMNPROPERTY( OBJECT_ID(QUOTENAME(COALESCE(@owner,USER_NAME())) + '.' + @table_name),SUBSTRING(@Column_Name,2,LEN(@Column_Name) - 2),'IsComputed')) = 1 
			BEGIN
				GOTO SKIP_LOOP					
			END
		END

		--Tables with columns of IMAGE data type are not supported for obvious reasons
		IF(@Data_Type in ('image'))
			BEGIN
				IF (@ommit_images = 0)
					BEGIN
						RAISERROR('Tables with image columns are not supported.',16,1)
						PRINT 'Use @ommit_images = 1 parameter to generate INSERTs for the rest of the columns.'
						PRINT 'DO NOT ommit Column List in the INSERT statements. If you ommit column list using @include_column_list=0, the generated INSERTs will fail.'
						RETURN -1 --Failure. Reason: There is a column with image data type
					END
				ELSE
					BEGIN
					GOTO SKIP_LOOP
					END
			END

		--Determining the data type of the column and depending on the data type, the VALUES part of
		--the INSERT statement is generated. Care is taken to handle columns with NULL values. Also
		--making sure, not to lose any data from flot, real, money, smallmomey, datetime columns
		SET @Actual_Values = @Actual_Values  +
		CASE 
			WHEN @Data_Type IN ('char','varchar','nchar','nvarchar') 
				THEN 
					'COALESCE('''''''' + REPLACE(RTRIM(' + @Column_Name + '),'''''''','''''''''''')+'''''''',''NULL'')'
			WHEN @Data_Type IN ('datetime','smalldatetime') 
				THEN 
					'COALESCE('''''''' + RTRIM(CONVERT(char,' + @Column_Name + ',109))+'''''''',''NULL'')'
			WHEN @Data_Type IN ('uniqueidentifier') 
				THEN  
					'COALESCE('''''''' + REPLACE(CONVERT(char(255),RTRIM(' + @Column_Name + ')),'''''''','''''''''''')+'''''''',''NULL'')'
			WHEN @Data_Type IN ('text','ntext') 
				THEN  
					'COALESCE('''''''' + REPLACE(CONVERT(char(8000),' + @Column_Name + '),'''''''','''''''''''')+'''''''',''NULL'')'					
			WHEN @Data_Type IN ('binary','varbinary') 
				THEN  
					'COALESCE(RTRIM(CONVERT(char,' + 'CONVERT(int,' + @Column_Name + '))),''NULL'')'  
			WHEN @Data_Type IN ('timestamp','rowversion') 
				THEN  
					CASE 
						WHEN @include_timestamp = 0 
							THEN 
								'''DEFAULT''' 
							ELSE 
								'COALESCE(RTRIM(CONVERT(char,' + 'CONVERT(int,' + @Column_Name + '))),''NULL'')'  
					END
			WHEN @Data_Type IN ('float','real','money','smallmoney')
				THEN
					'COALESCE(LTRIM(RTRIM(' + 'CONVERT(char, ' +  @Column_Name  + ',2)' + ')),''NULL'')' 
			ELSE 
				'COALESCE(LTRIM(RTRIM(' + 'CONVERT(char, ' +  @Column_Name  + ')' + ')),''NULL'')' 
		END   + '+' +  ''',''' + ' + '

		--Generating the column list for the INSERT statement
		SET @Column_List = @Column_List +  @Column_Name + ','	

		SKIP_LOOP: --The label used in GOTO

		SELECT 	@Column_ID = MIN(ORDINAL_POSITION) 
		FROM 	INFORMATION_SCHEMA.COLUMNS (NOLOCK) 
		WHERE 	TABLE_NAME = @table_name AND 
		ORDINAL_POSITION > @Column_ID AND
		(@owner IS NULL OR TABLE_SCHEMA = @owner)

	--Loop ends here!
	END

--To get rid of the extra characters that got concatenated during the last run through the loop
SET @Column_List = LEFT(@Column_List,len(@Column_List) - 1)
SET @Actual_Values = LEFT(@Actual_Values,len(@Actual_Values) - 6)

IF LTRIM(@Column_List) = '' 
	BEGIN
		RAISERROR('No columns to select. There should at least be one column to generate the output',16,1)
		RETURN -1 --Failure. Reason: Looks like all the columns are ommitted using the @cols_to_exclude parameter
	END

--Forming the final string that will be executed, to output the INSERT statements
IF (@include_column_list <> 0)
	BEGIN
		SET @Actual_Values = 
			'SELECT ' +  
			CASE WHEN @top IS NULL OR @top < 0="" then="" ''="" else="" '="" top="" '="" +="" ltrim(str(@top))="" +="" '="" '="" end="" +="" ''''="" +="" rtrim(@start_insert)="" +="" '="" ''+'="" +="" '''('="" +="" rtrim(@column_list)="" +="" '''+'="" +="" ''')'''="" +="" '="" +''values(''+="" '="" +="" @actual_values="" +="" '+'')'''="" +="" '="" '="" +="" coalesce(@from,'="" from="" '="" +="" case="" when="" @owner="" is="" null="" then="" ''="" else="" '['="" +="" ltrim(rtrim(@owner))="" +="" '].'="" end="" +="" '['="" +="" rtrim(@table_name)="" +="" ']'="" +="" '(nolock)')="" end="" else="" if="" (@include_column_list="0)" begin="" set="" @actual_values='SELECT ' +="" case="" when="" @top="" is="" null="" or="" @top="">< 0="" then="" ''="" else="" '="" top="" '="" +="" ltrim(str(@top))="" +="" '="" '="" end="" +="" ''''="" +="" rtrim(@start_insert)="" +="" '="" ''="" +''values(''+="" '="" +="" @actual_values="" +="" '+'')'''="" +="" '="" '="" +="" coalesce(@from,'="" from="" '="" +="" case="" when="" @owner="" is="" null="" then="" ''="" else="" '['="" +="" ltrim(rtrim(@owner))="" +="" '].'="" end="" +="" '['="" +="" rtrim(@table_name)="" +="" ']'="" +="" '(nolock)')="" end="" --determining="" whether="" to="" ouput="" any="" debug="" information="" if="" @debug_mode="1" begin="" print="" '/*****start="" of="" debug="" information*****'="" print="" 'beginning="" of="" the="" insert="" statement:'="" print="" @start_insert="" print="" ''="" print="" 'the="" column="" list:'="" print="" @column_list="" print="" ''="" print="" 'the="" select="" statement="" executed="" to="" generate="" the="" inserts'="" print="" @actual_values="" print="" ''="" print="" '*****end="" of="" debug="" information*****/'="" print="" ''="" end="" print="" '--inserts="" generated="" by="" ''sp_generate_inserts''="" stored="" procedure="" written="" by="" vyas'="" print="" '--build="" number:="" 22'="" print="" '--problems/suggestions?="" contact="" vyas="" @="" vyaskn@hotmail.com'="" print="" '--http://vyaskn.tripod.com'="" print="" ''="" print="" 'set="" nocount="" on'="" print="" ''="" --determining="" whether="" to="" print="" identity_insert="" or="" not="" if="" (@idn=""><> '')
	BEGIN
		PRINT 'SET IDENTITY_INSERT ' + QUOTENAME(COALESCE(@owner,USER_NAME())) + '.' + QUOTENAME(@table_name) + ' ON'
		PRINT 'GO'
		PRINT ''
	END

IF @disable_constraints = 1 AND (OBJECT_ID(QUOTENAME(COALESCE(@owner,USER_NAME())) + '.' + @table_name, 'U') IS NOT NULL)
	BEGIN
		IF @owner IS NULL
			BEGIN
				SELECT 	'ALTER TABLE ' + QUOTENAME(COALESCE(@target_table, @table_name)) + ' NOCHECK CONSTRAINT ALL' AS '--Code to disable constraints temporarily'
			END
		ELSE
			BEGIN
				SELECT 	'ALTER TABLE ' + QUOTENAME(@owner) + '.' + QUOTENAME(COALESCE(@target_table, @table_name)) + ' NOCHECK CONSTRAINT ALL' AS '--Code to disable constraints temporarily'
			END

		PRINT 'GO'
	END

PRINT ''
PRINT 'PRINT ''Inserting values into ' + '[' + RTRIM(COALESCE(@target_table,@table_name)) + ']' + ''''

--All the hard work pays off here!!! You'll get your INSERT statements, when the next line executes!
EXEC (@Actual_Values)

PRINT 'PRINT ''Done'''
PRINT ''

IF @disable_constraints = 1 AND (OBJECT_ID(QUOTENAME(COALESCE(@owner,USER_NAME())) + '.' + @table_name, 'U') IS NOT NULL)
	BEGIN
		IF @owner IS NULL
			BEGIN
				SELECT 	'ALTER TABLE ' + QUOTENAME(COALESCE(@target_table, @table_name)) + ' CHECK CONSTRAINT ALL'  AS '--Code to enable the previously disabled constraints'
			END
		ELSE
			BEGIN
				SELECT 	'ALTER TABLE ' + QUOTENAME(@owner) + '.' + QUOTENAME(COALESCE(@target_table, @table_name)) + ' CHECK CONSTRAINT ALL' AS '--Code to enable the previously disabled constraints'
			END

		PRINT 'GO'
	END

PRINT ''
IF (@IDN <> '')
	BEGIN
		PRINT 'SET IDENTITY_INSERT ' + QUOTENAME(COALESCE(@owner,USER_NAME())) + '.' + QUOTENAME(@table_name) + ' OFF'
		PRINT 'GO'
	END

PRINT 'SET NOCOUNT OFF'

SET NOCOUNT OFF
RETURN 0 --Success. We are done!
END

GO

PRINT 'Created the procedure'
GO

--Mark procedure as system object
EXEC sys.sp_MS_marksystemobject sp_generate_inserts
GO

PRINT 'Granting EXECUTE permission on sp_generate_inserts to all users'
GRANT EXEC ON sp_generate_inserts TO public

SET NOCOUNT OFF
GO

PRINT 'Done'
```

### Method 2

```js
IF EXISTS (SELECT * FROM sysobjects WHERE xtype = 'P' AND name = 'spu_GenerateInsert')
BEGIN
     DROP PROCEDURE spu_GenerateInsert
END
GO

CREATE PROCEDURE spu_GenerateInsert
     @table varchar(128), -- used to specify the table to generate data for
     @generateGo bit = 0, -- used to allow GO statements to separate the insert statements
     @restriction varchar(1000) = '', -- used to allow the data set to be restricted, no need for the where clause but can use syntax as 'columna = 1'
     @producesingleinsert bit = 0, -- used to switch the ability to produce multiple insert statements (default) or one statement using UNION SELECT
     @debug bit = 0, -- used to allow debugging to be turned on to the stored procedure - in case of queries
     @GenerateOneLinePerColumn bit = 0, -- used to display the columns and data on separate lines
     @GenerateIdentityColumn bit = 1 -- used to prevent the identity columns from being scripted
AS
/*******************************************************************************
Original Author:	Keith E Kratochvil

This version:		Jane Dallaway

Updates at:			http://jane.dallaway.com/downloads/SQL/spu_generateInsert.sql

Documentation at:	http://jane.dallaway.com/blog/labels/spu_generateinsert.html

Date Created:		March 16, 2000

Description:		This procedure takes the data from a table and turns it into 
					an insert statement.

CAUTION!!! If you run this on a large table be prepared to wait a while!

Modified:   add a comment here (date, who, comment)

Date        Name  Description
~~~~~~~     ~~~~~ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
07/11/03    Jane  Added a @generateGO parameter to allow selection
07/11/03    Jane  This procedure has an issue with NULLs....
07/11/03    Jane  Deal with Identities
07/11/03    Jane  Wrap all tablenames and columns with [ and ]
15/12/03    Jane  For DateTimes covert as style 1 - to allow for mm/dd/yyy
16/12/03    Jane  Get rid of rowcount
18/12/03    Jane  Prevent single field tables having that field displayed twice
06/07/04    Jane  Large money values get separeted with a comma - so specify convert
                  with 0 rather than 1         
31/05/05    Jane  Added default for GenerateGo and added ability to generate
                  Inserts for selected records based on the restriction
03/01/08    Jane  Updated to cope with text and ntext.  It converts to VARCHAR(8000) to allow quote escaping
                  Also copes with Nulls much better now.
07/01/08    Jane  Now handles guids
07/01/08    Jane  Forced collation to use database_default as was causing an error in some circumstances
15/01/08    Jane  Dave reported issue with image column types as a comment on my blog
                  http://jane.dallaway.com/blog/2007/11/generate-sql-insert-statement-from.html#c9038036788352783369
                  So, ensured that all column types either work, or replace with NULL and add warning
23/01/08    Jane  Ignore calculated columns.  Can't migrate the data, so remove from the INSERT
                  Implemented a suggestion from Jon Green - 4R Systems Inc left on my blog post at
                  http://jane.dallaway.com/blog/2007/11/generate-sql-insert-statement-from.html#c2055936172890486440
                  to allow a choice of separate insert statements or a single statement using the UNION SELECT syntax.
                  New parameter @producesingleinsert used.  When this is set to 0 it produces separate INSERT statements.
                  When set to 1 it produces a single statment using UNION SELECT
20/08/08 Jane     New parameter @GenerateOneLinePerColumn added as suggested by Christian via comment on my blog post at
                  http://jane.dallaway.com/blog/2007/11/generate-sql-insert-statement-from.html?showComment=1219174920000#c6992035307857457643
                  Also made all string variables varchar(max).  This means it no longer works on SQL 2000 - but to make it do so is just a case of
                  putting all varchar(max) to varchar(8000)
07/01/09 Jane     New parameter @GenerateIdentityColumns added as suggestion by James Bradshaw to enable identity columns to not be scripted
                  and therefore rely on the database to populate the identities from scratch
16/02/09 Jane     Continuation of work started on 20/08/08 - all remaining VARCHAR(8000)s removed and replaced with VARCHAR(max).  So, no longer
                  an issue with text columns unless it is SQL Server 2000, in which case this stored procedure will need to have been updated.  
16/04/09 Jane     Add checking to see if the table specified actually exists - user error on my case when using the procedure
17/04/09 Jane     Changed @tabledata to be nvarchar rather than varchar to allow for unicode                  
                  Added checking for data exceeding 8000 bytes and split the data based on CHAR(13) if this situation is seen.  
                  This won't resolve it in all cases, and if it doesn't then a warning is displayed at the bottom of the generated code
08/06/09 Jane     All strings are now output as N'<data>' rather than '<data>' to cope with extended character sets

Known Issues:     
     1) BLOBs can't be output

Usage:
     exec spu_GenerateInsert @table ='users', @generateGo=0, @restriction='columna = x', @producesingleinsert=0, @debug=0, @GenerateOneLinePerColumn=0, @GenerateIdentityColumn=0

Version:
     This version has been tested on SQL Server 2005.  To make this work on SQL Server 2000, replace all instances of VARCHAR(max) with VARCHAR(8000).  This will limit 
     the ability of export of text and XML columns to 8000 characters

*******************************************************************************/

--Variable declarations
DECLARE @InsertStmt varchar(max) -- change this to be (8000) for SQL Server 2000
DECLARE @Fields varchar(max) -- change this to be (8000) for SQL Server 2000
DECLARE @SelList varchar(max) -- change this to be (8000) for SQL Server 2000
DECLARE @Data varchar(max) -- change this to be (8000) for SQL Server 2000
DECLARE @ColName varchar(128)
DECLARE @IsChar tinyint
DECLARE @FldCounter int
DECLARE @TableData nvarchar(max) -- change this to be (8000) for SQL Server 2000

-- added by Jane - 07/11/03
DECLARE @bitIdentity BIT

-- added by Jane 03/01/08
DECLARE @bitHasEncounteredText BIT
SET @bitHasEncounteredText = 0

-- added by Jane 15/01/08
DECLARE @bitHasEncounteredImage BIT
SET @bitHasEncounteredImage = 0
DECLARE @bitHasEncounteredBinary BIT
SET @bitHasEncounteredBinary = 0
DECLARE @bitHasEncounteredXML BIT
SET @bitHasEncounteredXML = 0

-- added by Jane - 23/01/08
DECLARE @bitInsertStatementPrinted BIT
SET @bitInsertStatementPrinted = 0

-- added by Jane - 17/04/09 - To try and cope with bits of data which are greater than 8000 bytes
DECLARE @bitDataExceedMaxPrintLength BIT
SET @bitDataExceedMaxPrintLength = 0
DECLARE @cintMaximumSupportedPrintByteCount INT
SET @cintMaximumSupportedPrintByteCount = 8000 -- based on SQL Server 2005
DECLARE @statementToOutput NVARCHAR(max) -- change this to be (8000) for SQL Server 2000
DECLARE @NextCR INT -- used to split the output up into smaller chunks - look for carriage returns/line feeds and break into separate print statements
DECLARE @statementsToOutput TABLE (Id INT IDENTITY(1,1), singleStatement NVARCHAR (max) ) -- change this to be (8000) for SQL Server 2000
DECLARE @id INT
DECLARE @singleStatement NVARCHAR(max) -- change this to be (8000) for SQL Server 2000
DECLARE @loop INT

-- added by Jane - 16/12/03
SET NOCOUNT OFF

-- added by Jane - 16/04/09 - check for table existance
IF EXISTS(SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = @table)
BEGIN

     -- added by Jane - 16/04/2009 - Show details of table being generated, and date/time
     PRINT REPLICATE('-', 37 + LEN(@table) + LEN(CONVERT(VARCHAR,GETDATE(),120)))          
     PRINT '-- Script generated for table ' + @table + ' on ' + CONVERT(VARCHAR,GETDATE(),120) + ' --'
     PRINT REPLICATE('-', 37 + LEN(@table) + LEN(CONVERT(VARCHAR,GETDATE(),120)))

     -- added by Jane - 07/11/03
     SELECT @bitIdentity = OBJECTPROPERTY(OBJECT_ID(TABLE_NAME), 'TableHasIdentity')
     FROM INFORMATION_SCHEMA.TABLES
     WHERE TABLE_Name =@table

     -- added by Jane - 03/01/08
     PRINT '-- ** Start of Inserts ** --'
     PRINT ''

     -- added by Jane - 07/11/03
     -- AND @GenerateIdentityColumn = 1 added by Jane - 07/01/09
     IF @bitIdentity = 1 AND @GenerateIdentityColumn = 1
     BEGIN
           PRINT 'SET IDENTITY_INSERT [' + @table + '] ON '
     END

     --initialize some of the variables
     -- updated by Jane 20/08/08 added one line per column functionality as per Christian's suggestion
     SELECT @InsertStmt = 'INSERT INTO [' + @Table + '] '+ CASE WHEN @GenerateOneLinePerColumn = 1 THEN CHAR(13) ELSE '' END + '(' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN CHAR(13) ELSE '' END,
           @Fields = '',
           @Data = '',
           @SelList = 'SELECT ',
           @FldCounter = 0

     --create a cursor that loops through the fields in the table
     --and retrieves the column names and determines the delimiter type that the
     --field needs
     DECLARE CR_Table CURSOR FAST_FORWARD FOR

           SELECT COLUMN_NAME,
                  'IsChar' = CASE
                  WHEN DATA_TYPE in ('int', 'money', 'decimal', 'tinyint', 'smallint' ,'numeric', 'bit', 'bigint', 'smallmoney', 'float','timestamp') THEN 0
                  WHEN DATA_TYPE in ('char', 'varchar', 'nvarchar','uniqueidentifier', 'nchar') THEN 1
                  WHEN DATA_TYPE in ('datetime', 'smalldatetime') THEN 2
                  WHEN DATA_TYPE in ('text', 'ntext') THEN 3
                  WHEN DATA_TYPE in ('image') THEN 4 -- added by Jane - 15/01/08
                  WHEN DATA_TYPE in ('binary', 'varbinary') THEN 5 -- added by Jane - 15/01/08
                  WHEN DATA_TYPE in ('sql_variant') THEN 6 -- added by Jane - 15/01/08 - Force to be converted as varchars
                  WHEN DATA_TYPE in ('xml') THEN 7 -- added by Jane - 15/01/08
                  ELSE 9
           END
           FROM INFORMATION_SCHEMA.COLUMNS c WITH (NOLOCK)
           INNER JOIN syscolumns sc WITH (NOLOCK)
           ON c.COLUMN_NAME = sc.name
           INNER JOIN sysobjects so WITH (NOLOCK)
           ON sc.id = so.id
           AND so.name = c.TABLE_NAME
           WHERE table_name = @table
           AND DATA_TYPE <>'timestamp'
           AND sc.IsComputed = 0      
           AND 1 = 
               CASE @GenerateIdentityColumn 
               WHEN 1 -- When we want the identity columns to be generated, then always include the column
               THEN 1 
               ELSE 
                    CASE COLUMNPROPERTY(object_id(TABLE_NAME), COLUMN_NAME, 'IsIdentity') -- Check if the column has the property IsIdentity
                    WHEN 1 -- If it does
                    THEN 0 -- don't include this column
                    ELSE 1 -- otherwise include this column
                    END
               END
           ORDER BY ORDINAL_POSITION
           FOR READ ONLY
           OPEN CR_Table

           FETCH NEXT FROM CR_Table INTO @ColName, @IsChar

     WHILE (@@fetch_status <> -1)
     BEGIN

           IF @IsChar = 3
                  SET @bitHasEncounteredText = 1           

           -- added by Jane - 15/01/08
           IF @IsChar = 4
                  SET @bitHasEncounteredImage = 1
           IF @IsChar = 5
                  SET @bitHasEncounteredBinary = 1

           IF (@@fetch_status <> -2)
           BEGIN

                  -- Updated by Jane - 15/01/08 - cope with xml, image, binary, varbinary etc
                  -- Updated by Jane - 03/01/08 to cope with text and ntext - converts to VARCHAR(8000) to allow quote escaping
                  -- Special case for first field
                  IF @FldCounter = 0
                  BEGIN
                          SELECT @Fields =  @Fields + '[' + @ColName + ']' + ', '
                          -- Updated by Jane - 08/06/09 - prefix string with N to cope with extended character sets                          
                          SELECT @SelList =  CASE @IsChar
                                 WHEN 1 THEN @SelList +  ' ISNULL(''N'''''' + REPLACE(['+  @ColName + '],'''''''', '''''''''''') + '''''''' ,''NULL'')  ' + ' COLLATE database_default + '
                                 WHEN 2 THEN @SelList +  ' ISNULL(''N'''''' + CONVERT(varchar(20),[' + @ColName + ']) + '''''''',''NULL'') ' + ' COLLATE database_default + '
                                 WHEN 3 THEN @SelList +  ' ISNULL(''N'''''' + REPLACE(CONVERT(VARCHAR(max),['+  @ColName + ']),'''''''', '''''''''''')+  '''''''' ,''NULL'')  '+ ' COLLATE database_default + '
                                 WHEN 4 THEN @SelList + '''NULL''' + ' COLLATE database_default + '
                                 WHEN 5 THEN @SelList + '''NULL''' + ' COLLATE database_default + '
                                 WHEN 6 THEN @SelList +  ' ISNULL(''N'''''' + REPLACE(CONVERT(VARCHAR(max),['+  @ColName + ']),'''''''', '''''''''''')+  '''''''' ,''NULL'')  '+ ' COLLATE database_default + '
                                 WHEN 7 THEN @SelList +  ' ISNULL(''N'''''' + REPLACE(CONVERT(VARCHAR(max),['+  @ColName + ']),'''''''', '''''''''''')+  '''''''' ,''NULL'')  '+ ' COLLATE database_default + '
                                 ELSE @SelList + 'ISNULL(CONVERT(varchar(2000),['+@ColName + '],0),''NULL'')' + ' COLLATE database_default + '
                                 END
                          SELECT @FldCounter = @FldCounter + 1
                          SET @SelList = @Sellist
                          FETCH NEXT FROM CR_Table INTO @ColName, @IsChar
                  END

                  -- Updated by Jane - 15/01/08 - cope with xml, image, binary, varbinary etc
                  -- Updated by Jane - 03/01/08 to cope with NULL replacements           
                  -- Updated by Jane - 03/01/08 to cope with text and ntext - converts to VARCHAR(8000) to allow quote escaping
                  -- Updated by Jane - 18/12/03 to prevent single field tables having that field displayed twice
                  -- Updated by Jane - 20/08/08 to incorporate the @GenerateOneLinePerColumn parameter suggested by Christian
                  IF @@fetch_status <> -1
                  BEGIN
                          SELECT @Fields =  @Fields + '[' + @ColName + ']' + ', '
                          -- Updated by Jane - 08/06/09 - prefix string with N to cope with extended character sets
                          SELECT @SelList =  CASE @IsChar
                                 WHEN 1 THEN @SelList +  ''',''' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN ' + CHAR(13) ' ELSE '' END + ' + ' +  ' ISNULL(''N'''''' + REPLACE(['+  @ColName + '],'''''''', '''''''''''' ) +  '''''''',''NULL'') ' + ' COLLATE database_default + '
                                 WHEN 2 THEN @SelList + ''',''' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN  ' + CHAR(13) ' ELSE '' END + ' + '  +  'ISNULL(''N'''''' + CONVERT(varchar(20),['+ @ColName + '])+ '''''''',''NULL'') ' + ' COLLATE database_default + '
                                 WHEN 3 THEN @SelList +  ''',''' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN ' + CHAR(13) ' ELSE '' END + ' + ' +  ' ISNULL(''N'''''' + REPLACE(CONVERT(VARCHAR(max),['+  @ColName + ']),'''''''', '''''''''''' )+  '''''''',''NULL'')  ' + ' COLLATE database_default + '
                                 WHEN 4 THEN @SelList + ''',''' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN  ' + CHAR(13) ' ELSE '' END + ' + ' +  '''NULL''' + ' COLLATE database_default + '
                                 WHEN 5 THEN @SelList + ''',''' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN  ' + CHAR(13) ' ELSE '' END + ' + ' +  '''NULL''' + ' COLLATE database_default + '
                                 WHEN 6 THEN @SelList + ''',''' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN  ' + CHAR(13) ' ELSE '' END + ' + ' +   ' ISNULL(''N'''''' + REPLACE(CONVERT(VARCHAR(max),['+  @ColName + ']),'''''''', '''''''''''')+  '''''''' ,''NULL'')  '+ ' COLLATE database_default + '
                                 WHEN 7 THEN @SelList + ''',''' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN  ' + CHAR(13) ' ELSE '' END + ' + ' +   ' ISNULL(''N'''''' + REPLACE(CONVERT(VARCHAR(max),['+  @ColName + ']),'''''''', '''''''''''')+  '''''''' ,''NULL'')  '+ ' COLLATE database_default + '
                                 ELSE @SelList  + ''',''' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN  ' + CHAR(13) ' ELSE '' END + ' + ' + ' ISNULL(CONVERT(varchar(2000),['+@ColName + '],0),''NULL'')' + ' COLLATE database_default + '
                          END  
                  END
           END  

           FETCH NEXT FROM CR_Table INTO @ColName, @IsChar
     END

     CLOSE CR_Table
     DEALLOCATE CR_Table

     SELECT @Fields =  SUBSTRING(@Fields, 1,(len(@Fields)-1))

     SELECT @SelList =  SUBSTRING(@SelList, 1,(len(@SelList)-1))
     SELECT @SelList = @SelList + ' FROM ' + @table

     IF LEN(@restriction) > 0
     BEGIN
           SELECT @SelList = @SelList + ' WHERE ' + @restriction
     END

     -- updated by Jane 20/08/08 added one line per column functionality as per Christian's suggestion
     SELECT @InsertStmt = @InsertStmt + CASE WHEN @GenerateOneLinePerColumn = 1 THEN REPLACE(@Fields,', ',',' + CHAR(13)) ELSE @Fields END + CASE WHEN @GenerateOneLinePerColumn = 1 THEN CHAR(13) ELSE '' END + ')'

     --for debugging purposes...
     IF @Debug = 1
     BEGIN
           PRINT '*** DEBUG INFORMATION - THIS IS THE SELECT STATEMENT BEING RUN *** '
           PRINT @sellist
           PRINT '*** END DEBUG ***'
     END

     -- added by Jane - 16/12/03
     SET NOCOUNT ON

     --now we need to create and load the temp table that will hold the data
     --that we are going to generate into an insert statement

     CREATE TABLE #TheData (TableData VARCHAR(max)) -- change this to be (8000) for SQL Server 2000
     INSERT INTO #TheData (TableData) EXEC (@SelList)

     --Cursor through the data to generate the INSERT statement / VALUES/SELECT/UNION SELECT clause
     DECLARE CR_Data CURSOR FAST_FORWARD FOR SELECT TableData FROM #TheData FOR
     READ ONLY
     OPEN CR_Data
     FETCH NEXT FROM CR_Data INTO @TableData

           WHILE (@@fetch_status <> -1)
           BEGIN
                 IF (@@fetch_status <> -2)
                 BEGIN                                            

                       -- Updated by Jane 17/04/09 instead of printing at this point, store the output in a @statementToOutput variable.  This allows us to try and split it to 
                       -- to print within the 8000 byte limit imposed by the PRINT function			
                       -- Updated by Jane 23/01/08 after suggestion posted to blog at http://jane.dallaway.com/blog/2007/11/generate-sql-insert-statement-from.html#c2055936172890486440
                       IF (@producesingleinsert = 1 )
                              IF (@bitInsertStatementPrinted = 0)
                              BEGIN
									SET @statementToOutput = @InsertStmt + char(13) + 'SELECT ' + @TableData                                    
                                    SET @bitInsertStatementPrinted = 1
                              END
                              ELSE
                              BEGIN
									SET @statementToOutput = 'UNION SELECT ' + @TableData
                              END
                       ELSE
                       BEGIN
                              -- updated by Jane 20/08/08 added one line per column functionality as per Christian's suggestion
                              SET @statementToOutput =  @InsertStmt + CASE WHEN @GenerateOneLinePerColumn = 1 THEN CHAR(13) ELSE '' END + 'VALUES ' + + CASE WHEN @GenerateOneLinePerColumn = 1 THEN CHAR(13) ELSE '' END + '(' + CASE WHEN @GenerateOneLinePerColumn = 1 THEN CHAR(13) ELSE '' END + @TableData + CASE WHEN @GenerateOneLinePerColumn = 1 THEN CHAR(13) ELSE '' END + ')' + CHAR(13)
                       END

                       -- Added by Jane - 17/04/09 - check for length of @statementToOutput
                       -- if it exceeds the maximum length, then lets attempt to split it on CRs as these will be done via separate PRINT statements
                       IF DATALENGTH(@statementToOutput) > @cintMaximumSupportedPrintByteCount                                                                                                                     
                       BEGIN                                                      

                           -- Break the @statementToOutput based on CHAR(13) and put separate data values into @statementsToOutput table

                           -- Get rid of double line breaks
                           -- Replace CHAR(10) with CHAR(13)
                           SET @statementToOutput = REPLACE(@statementToOutput,CHAR(10),CHAR(13))
                           -- Replace CHAR(13)+CHAR(13) with CHAR(13)
                           SET @statementToOutput = REPLACE(@statementToOutput,CHAR(13)+CHAR(13),CHAR(13))

                           SET @NextCR = Charindex(CHAR(13),@statementToOutput)
                           WHILE @NextCR  > 0
                           BEGIN

                               INSERT INTO @statementsToOutput VALUES(LEFT(@statementToOutput,@NextCR - 1))

                               SET @statementToOutput = Right(@statementToOutput,Len(@statementToOutput) - @NextCR)
                               SET @NextCR = Charindex(CHAR(13),@statementToOutput)
                           END                           						   
                           INSERT INTO @statementsToOutput VALUES(@statementToOutput)				                                                                   

                           -- Output the statements line by line
						   SET @loop = 1
						   SET @id = -1

						   WHILE @loop = 1
						   BEGIN
                               SELECT TOP 1 @id = Id, @singleStatement = singlestatement
                               FROM @statementsToOutput
                               WHERE id > @id
                               ORDER BY Id

                               SET @loop = @@ROWCOUNT

                               IF @loop = 0
                                    BREAK

                               -- No guarantee that we still don't exceed the limits, but should have more of a chance of avoiding them
                               IF DATALENGTH(@singleStatement) > @cintMaximumSupportedPrintByteCount
                               BEGIN
                                    SET @bitDataExceedMaxPrintLength = 1
                                    SELECT @singleStatement                           
                               END

                               PRINT @singleStatement
						   END													   
                       END    
                       ELSE
                       BEGIN					
                           -- Don't need to worry, we haven't exceeded the 8000 byte limit so just print it
						   PRINT @statementToOutput 
                       END

                       IF @generateGo = 1
                       BEGIN
                              PRINT 'GO'
                       END
                 END
                 FETCH NEXT FROM CR_Data INTO @TableData
           END
     CLOSE CR_Data
     DEALLOCATE CR_Data

     -- added by Jane - 07/11/03
     -- AND @GenerateIdentityColumn = 1 added by Jane - 07/01/09
     IF @bitIdentity = 1 AND @GenerateIdentityColumn = 1
     BEGIN
           PRINT 'SET IDENTITY_INSERT [' + @table + '] OFF '
     END

     -- added by Jane - 03/01/08
     PRINT '-- ** End of Inserts ** --'

     IF @bitHasEncounteredImage = 1
     BEGIN
           PRINT '-- ** WARNING: There is an image column in your table which has not been migrated - this has been replaced with NULL.  You will need to do this by hand.  Images are not supported by this script at this time.  ** --'
     END

     -- added by Jane - 15/01/08
     IF @bitHasEncounteredBinary = 1
     BEGIN
           PRINT '-- ** WARNING: There is a binary or varbinary column in your table which has not been migrated - this has been replaced with NULL.  You will need to do this by hand.  Binary and VarBinary are not supported by this script at this time.  ** --'
     END

     -- 16/02/09 - These checks are only required if the database is SQL Server 2000
     DECLARE @Version VARCHAR(100)
     SELECT @Version = @@VERSION
     IF PATINDEX('%8.00%',@Version) > 0
     BEGIN
          IF @bitHasEncounteredXML = 1
          BEGIN
                PRINT '-- ** WARNING: This will convert any ''xml'' data to be ''varchar(8000)'' ** --'
          END

          -- added by Jane - 03/01/08
          IF @bitHasEncounteredText = 1 
          BEGIN
                PRINT '-- ** WARNING: This will convert any ''text'' or ''ntext'' data to be ''varchar(8000)'' ** --'
          END
     END

     IF @bitDataExceedMaxPrintLength = 1
     BEGIN
          PRINT '-- ** WARNING: The data length for at least one row exceeds '+ CONVERT(VARCHAR(6),@cintMaximumSupportedPrintByteCount) + ' bytes.  The PRINT command is limited to ' + CONVERT(VARCHAR(6),@cintMaximumSupportedPrintByteCount) + ' bytes (for more information see http://msdn.microsoft.com/en-us/library/ms176047.aspx).  Do not trust this data. ** --'
     END
END
ELSE
BEGIN

     -- added by Jane - 16/04/2009 - Warn user that table doesn't exist
     PRINT REPLICATE('-', 43 + LEN(@table))     
     PRINT '-- Table ' + @table + ' doesn''t exist on this database --'
     PRINT REPLICATE('-', 43 + LEN(@table))

END 
RETURN (0)

GO
```</data></data>

origin - http://www.pipiscrew.com/?p=2783 sql-generate-scripts-alternative