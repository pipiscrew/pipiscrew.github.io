---
title: Generate HTML table from list of generic class with specified properties
author: PipisCrew
date: 2019-05-23
categories: [.net]
toc: true
---

https://stackoverflow.com/questions/11126137/generate-html-table-from-list-of-generic-class-with-specified-properties

compact version :
```js
StringBuilder sb = new StringBuilder();
sb.Append("<table>");
foreach(var item in MyList){
    sb.AppendFormat("<tr><td>{0}</td></tr>", item);
}
sb.Append("</table>");
```

origin - https://www.pipiscrew.com/?p=14935 generate-html-table-from-list-of-generic-class-with-specified-properties