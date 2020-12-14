---
title: mysql loop through records procedure
author: PipisCrew
date: 2019-12-06
categories: [sql]
toc: true
---

## using while

```js
DELIMITER //

CREATE PROCEDURE test4 ()
BEGIN
DECLARE paymentsSize INT DEFAULT 0;
DECLARE i INT DEFAULT 0;

select count(*) from payments into paymentsSize;

while i<paymentsSize DO

  insert into `payments_info` (`address`,`payment_id`) select 'Pentelis',id FROM payments LIMIT i,1;

  SET i = i + 1;
END WHILE;
END //

DELIMITER ;
```

## using cursor

```js
--src - http://www.markomedia.com.au/mysql-cursors-in-stored-procedures/

DELIMITER // 

DROP PROCEDURE IF EXISTS sp_test //

CREATE PROCEDURE sp_test ()
BEGIN
	DECLARE done INT DEFAULT FALSE;
	DECLARE myid INT;
	DECLARE cur1 CURSOR FOR SELECT id from table1 WHERE firstname IS NULL;
	DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

	OPEN cur1;

	read_loop: LOOP
		IF done THEN
			LEAVE read_loop;
		END IF;

		FETCH cur1 INTO myid;
		UPDATE table1 SET firstname = (SELECT firstname from table2 WHERE id = myid)
		WHERE id = myid;
	END LOOP;

	close cur1;
END;
```

origin - https://www.pipiscrew.com/?p=16226 mysql-loop-through-records-procedure