---
title: Merge tables
author: PipisCrew
date: 2020-07-27
categories: [sql]
toc: true
---

![](https://i.imgur.com/DDSOQ2L.png)

you have two table called source and target tables, and you need to update the target table based on the values matched from the source table. There are three cases:

1- The source table has some rows that do not exist in the target table. In this case, you need to insert rows that are in the source table into the target table.
2- The target table has some rows that do not exist in the source table. In this case, you need to delete rows from the target table.
3- The source table has some rows with the same keys as the rows in the target table. However, these rows have different values in the non-key columns. In this case, you need to update the rows in the target table with the values coming from the source table.

![](https://i.imgur.com/wEJ9Ca3.png)

src - https://www.sqlservertutorial.net/sql-server-basics/sql-server-merge/

```js
MERGE ProductsLocalized t

USING (

              SELECT df.recid, turrican_code, caption_gr, description_gr, caption_en, description_en FROM dbo.xlsReference AS sql2008
              INNER JOIN tmp_products AS XLSProducts ON XLSProducts.code = sql2008.agony_code collate Greek_CI_AS
              INNER JOIN products AS df ON df.RecCode = sql2008.turrican_code --get the recid by here

) s

ON ( s.recid = t.productrecid AND t.languageid=1 )

WHEN MATCHED

    THEN UPDATE SET

        t.name = s.caption_gr,
        t.LargeDescription = s.description_gr;

--WHEN NOT MATCHED BY TARGET
--    THEN INSERT (Productrecid, LanguageId, title , LargeDescription)
--         VALUES (recid, 1, s.caption_gr, s.description_gr);
```

**Problem with linked servers**

    Msg 5315, Level 16, State 1, Line 77
    The target of a MERGE statement cannot be a remote table, a remote view, or a view over remote tables.

**Solution** 

The target of a MERGE cannot be remote, but the source of a MERGE can be remote. **So build the TSQL on TARGET server**!!!!!!!!

src - https://stackoverflow.com/a/19818924

origin - https://www.pipiscrew.com/?p=18745 merge-tables