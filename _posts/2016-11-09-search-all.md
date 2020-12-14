---
title: Search all tables all fields on Oracle dbase
author: PipisCrew
date: 2016-11-09
categories: [sql]
toc: true
---

```js
--source : http://stackoverflow.com/a/208892
    SET SERVEROUTPUT ON SIZE 100000

    DECLARE
      match_count INTEGER;
    BEGIN
      FOR t IN (SELECT owner, table_name, column_name
                  FROM all_tab_columns
                  WHERE owner <> 'SYS' and data_type LIKE '%CHAR%') LOOP

        EXECUTE IMMEDIATE
          'SELECT COUNT(*) FROM ' || t.owner || '.' || t.table_name ||
          ' WHERE '||t.column_name||' = :1'
          INTO match_count
          USING '1/22/2008P09RR8';

        IF match_count > 0 THEN
          dbms_output.put_line( t.table_name ||' '||t.column_name||' '||match_count );
        END IF;

      END LOOP;

    END;
```

origin - http://www.pipiscrew.com/?p=6257 search-all-tables-all-fields-on-oracle-dbase