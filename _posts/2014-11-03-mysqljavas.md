---
title: o[mysql+javascript] mysql datetime field to javascript - format date (+bootstrap-table)
author: PipisCrew
date: 2014-11-03
categories: []
toc: true
---

reference
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString)

**mysql** yyyy-mm-dd 
![](https://www.pipiscrew.com/wp-content/uploads/2014/11/snap140.png "snap140")

**pure js - no external library required**
```js
				function date_formatter(value, row) {
					if (value==null)
						return "";

					var date = new Date(value);
					var options = {
					    year: "numeric", month: "2-digit",
					    day: "2-digit", hour: "2-digit", minute: "2-digit", hour12: false
					};

					return(date.toLocaleString("en-GB", options));
				}
```

**using it** via **bootstap-table**
```js
			<table id="logger_tbl" data-toggle="table" data-striped="true" data-url="x_pagination.php" data-pagination="true" data-page-size="50"></table>
 			   data-sort-name="log_UTC_when" data-sort-order="desc"

	           data-side-pagination="server"
	           data-query-params="queryParamsLOGGER">

				<thead>
					<tr>
															<!-- using data-formatter attribute -->
						<th data-field="log_UTC_when" data-formatter="date_formatter" data-sortable="true">
							Date UTC
						</th>
					</tr>
				</thead>

```
**locales:**
```js
af-ZA
ca-CA
cs-CZ
da-DK
de-CH
de-DE
el-GR
en-GB
en-US
es-AR
es-ES
es-VE
et-EE
fi-FI
fr-FR
he-IL
hu-HU
it-IT
ja-JP
nl-NL
no-NO
pl-PL
pt-BR
pt-PT
ru-RU
sk-SK
sl-SI
sv-SE
tr-TR
uk-UA
zh-CH
```

origin - http://www.pipiscrew.com/?p=1680 mysqljavascript-mysql-datetime-field-to-javascript-format-date