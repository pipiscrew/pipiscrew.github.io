---
title: MySQLDumper
author: PipisCrew
date: 2015-04-02
categories: []
toc: true
---

Is a PHP and Perl based tool for backing up MySQL databases.

[http://www.mysqldumper.net/](http://www.mysqldumper.net/)

similar - 
[http://sypex.net/](http://sypex.net/)
warning doesnt backup the table schemas - [http://sypex.net/en/products/dumper/compare/](http://sypex.net/en/products/dumper/compare/)

otherwise use :
```js
<?php ref="" :="" http://davidwalsh.name/backup-mysql-database-php="" backup_tables('localhost','x','x','x');="" *="" backup="" the="" db="" or="" just="" a="" table="" */="" function="" backup_tables($host,$user,$pass,$name,$tables='*' )="" {="" $link="mysql_connect($host,$user,$pass);" mysql_select_db($name,$link);="" mysql_query("set="" character_set_results='utf8' ,="" character_set_client='utf8' ,="" character_set_connection='utf8' ,="" character_set_database='utf8' ,="" character_set_server='utf8' ");="" get="" all="" of="" the="" tables="" if($tables="=" '*')="" {="" $tables="array();" $result="mysql_query('SHOW" tables');="" while($row="mysql_fetch_row($result))" {="" $tables[]="$row[0];" }="" }="" else="" {="" $tables="is_array($tables)" $tables="" :="" explode(',',$tables);="" }="" cycle="" through="" foreach($tables="" as="" $table)="" {="" $result="mysql_query('SELECT" *="" from="" '.$table);="" $num_fields="mysql_num_fields($result);" $return.='DROP TABLE ' .$table.';';="" $row2="mysql_fetch_row(mysql_query('SHOW" create="" table="" '.$table));="" $return.="\n\n" .$row2[1].";\n\n";="" for="" ($i="0;" $i=""?>< $num_fields;="" $i++)="" {="" while($row="mysql_fetch_row($result))" {="" $return.='INSERT INTO ' .$table.'="" values(';="" for($j="0;"><$num_fields; $j++)="" {="" $row[$j]="addslashes($row[$j]);" $row[$j]="ereg_replace("\n","\\n",$row[$j]);" if="" (isset($row[$j]))="" {="" $return.='"' .$row[$j].'"'="" ;="" }="" else="" {="" $return.='""' ;="" }="" if=""></$num_fields;><($num_fields-1)) {="" $return.=',' ;="" }="" }="" $return.=");\n" ;="" }="" }="" $return.="\n\n\n" ;="" }="" ------------="" *="" backup="" procedure="" structure*/="" $result="mysql_query('SHOW" procedure="" status');="" while($row="mysql_fetch_row($result))" {="" $procedures[]="$row[1];" }="" foreach($procedures="" as="" $proc)="" {="" $return.="\n\nDELIMITER $$\n\n" ;="" $return.="DROP PROCEDURE IF EXISTS $name.$proc$$\n" ;="" $rowx="mysql_fetch_row(mysql_query("SHOW" create="" procedure="" $proc"));="" $return.="\n" .$rowx[2]."$$\n\n";="" $return.="DELIMITER ;\n\n" ;="" }="" ------------="" *="" backup="" procedure="" structure*/="" save="" file="" $handle="fopen('db-backup-'.time().'-'.(md5(implode(',',$tables))).'.sql','w+');" fwrite($handle,$return);="" fclose($handle);="" header('content-type:="" text/html;="" charset="utf-8');" echo="" $return;="" }=""></($num_fields-1))>
```

origin - http://www.pipiscrew.com/?p=1779 mysqldumper