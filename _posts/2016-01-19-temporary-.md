---
title: temporary table + cursor loop
author: PipisCrew
date: 2016-01-19
categories: [sql]
toc: true
---

reference -- [http://msdn.microsoft.com/en-us/library/ms180169.aspx](http://msdn.microsoft.com/en-us/library/ms180169.aspx)

```js
--variable
DECLARE @TBL_STR nvarchar(255)

--IF TEMPORARY TABLE EXISTS DROP IT!!
IF object_id('tempdb..#RESULTSET') IS NOT NULL
BEGIN
   DROP TABLE #RESULTSET
END

----CLOSE THE CURSOR, IF IT IS EMPTY THEN DEALLOCATE IT
IF (SELECT CURSOR_STATUS('global','rec_cursor')) >= -1
 BEGIN
  IF (SELECT CURSOR_STATUS('global','rec_cursor')) > -1
   BEGIN
    CLOSE rec_cursor
   END
 DEALLOCATE rec_cursor
END

--CREATE TEMPORARY TABLE
CREATE TABLE #RESULTSET
( TBL_STR nvarchar(255) );

--INSERT VALUES TO TEMPORARY
insert into #RESULTSET values ('cat1');
insert into #RESULTSET values ('cat2');
insert into #RESULTSET values ('cat3');

--GET ALL TEMPORARY RECORDS
DECLARE rec_cursor CURSOR FOR
	SELECT * FROM #RESULTSET

OPEN rec_cursor;
--GET ALL TEMPORARY RECORDS

--get the first record
FETCH NEXT FROM rec_cursor
INTO @TBL_STR;

--FOR ALL RECORDS IN ORDERS
WHILE @@FETCH_STATUS = 0
BEGIN
	insert into aa (aa_title) values (@TBL_STR);

	FETCH NEXT FROM rec_cursor
	INTO @TBL_STR;
END
```

the same with execute dynamic SQL 

```js
--variable
DECLARE @TBL_STR nvarchar(255)

--IF TEMPORARY TABLE EXISTS DROP IT!!
IF object_id('tempdb..#RESULTSET') IS NOT NULL
BEGIN
   DROP TABLE #RESULTSET
END

----CLOSE THE CURSOR, IF IT IS EMPTY THEN DEALLOCATE IT
IF (SELECT CURSOR_STATUS('global','rec_cursor')) >= -1
 BEGIN
  IF (SELECT CURSOR_STATUS('global','rec_cursor')) > -1
   BEGIN
    CLOSE rec_cursor
   END
 DEALLOCATE rec_cursor
END

--CREATE TEMPORARY TABLE
CREATE TABLE #RESULTSET
( TBL_STR nvarchar(255) );

--INSERT VALUES TO TEMPORARY
insert into #RESULTSET values ('cat1');
insert into #RESULTSET values ('cat2');
insert into #RESULTSET values ('cat3');

--GET ALL TEMPORARY RECORDS
DECLARE rec_cursor CURSOR FOR
	SELECT * FROM #RESULTSET

OPEN rec_cursor;
--GET ALL TEMPORARY RECORDS

--get the first record
FETCH NEXT FROM rec_cursor
INTO @TBL_STR;

--VARIABLE FOR SQL EXECUTION
Declare @Sql nvarchar(max)

--FOR ALL RECORDS IN ORDERS
WHILE @@FETCH_STATUS = 0
BEGIN
	--SET SQL VARIABLE (WARNING : dont use double quote, but double single quote aka '')
	Set @Sql = 'Declare @' + (@TBL_STR) + 'Id int 
			Set @' + (@TBL_STR) + 'Id = (Select PlayerX_Id from PlayerXs Where PlayerX_Code=''' + (@TBL_STR) + ''') 

			Insert Into PLAYERS(Player_ID, PlayerX_ID,PlayerXValueW,PlayerXY) 
			Select p.Player_ID, @' + (@TBL_STR) + 'Id, 1, Convert(nvarchar(10), p.Player_ID) + ''-'' + Convert(nvarchar(10),@' + (@TBL_STR) + 'Id) 
			from SOLO_Players sp 
			Inner Join Players p on p.Player_Q_ID=sp.ID 
			Where p.Player_ID not in 
					(Select Player_ID from PLAYERS Where PlayerXY=Convert(nvarchar(10), p.Player_ID) + ''-'' + Convert(nvarchar(10),@' + (@TBL_STR) + 'Id)) 
	  '
	--print @Sql
	--return
	exec (@Sql) --DYNAMIC SQL EXECUTION

	FETCH NEXT FROM rec_cursor
	INTO @TBL_STR;
END
```

### using multiple fields

```js
--using multiple fields into while, and assign them to variables
--VARIABLES FOR ORDER
DECLARE @CUSTOMER VARCHAR(255),
        @PriceListS_ID INT,
		@customer_id INT,
		@voucher_COUNTER INT,
		@ORDER_ID INT,
        @ORDER_DATE SMALLDATETIME,

--GET SPECIFIC ORDERS WITH 666
DECLARE orders_cursor CURSOR FOR
SELECT TOP 100 table_id,date,counter,fullname FROM orders WHERE voucher = @voucher_666

OPEN orders_cursor;

FETCH NEXT FROM orders_cursor
INTO @ORDER_ID, @ORDER_DATE,@voucher_COUNTER,@customer_id;
--GET SPECIFIC ORDERS WITH @voucher_666

--FOR ALL RECORDS IN ORDERS
WHILE @@FETCH_STATUS = 0
BEGIN

    --GET&SET CUSTOMER NAME +  PriceList ID
        SELECT @CUSTOMER=fullname,@PriceListS_ID=PriceLists FROM customers WHERE table_id=@customer_id

    --MOVE NEXT ORDERS
    FETCH NEXT FROM orders_cursor
    INTO @ORDER_ID, @ORDER_DATE,@voucher_COUNTER,@customer_id;
END
```

origin - http://www.pipiscrew.com/?p=2620 sql-temporary-table-cursor-loop