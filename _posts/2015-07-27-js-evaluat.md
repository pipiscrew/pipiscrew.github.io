---
title: JS Evaluate
author: PipisCrew
date: 2015-07-27
categories: []
toc: true
---

reference 
[http://weblog.west-wind.com/posts/2007/Feb/14/Evaluating-JavaScript-code-from-C](http://weblog.west-wind.com/posts/2007/Feb/14/Evaluating-JavaScript-code-from-C)

![](https://www.pipiscrew.com/wp-content/uploads/2015/07/snap134.png "snap134")

```js
using System;
using System.Web.Script.Serialization; //System.Web.Extensions.dll
using System.Windows.Forms;
using Microsoft.JScript; //Microsoft.JScript.dll

namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();

            for (int i = 0; i < 5;="" i++)="" {="" listbox1.items.add(i);="" }="" }="" private="" void="" button2_click(object="" sender,="" eventargs="" e)="" {="" try="" {="" string="" script="@" function"="" xor_str(str)="" {="" var="" xor_key="2;" var="" the_res='' ;="" var="" i;="" for(i=""><str.length;++i) {="" the_res+="String.fromCharCode(xor_key^str.charCodeAt(i));" }="" return="" the_res;="" };";="" xor="" function="" in="" js="" w/="" xor_key="2" script="" +="var q = " +="" tojson(listbox1.items)="" +="" ";";="" convert="" 'c#="" listbox'="" items="" to="" json="" and="" store="" it="" to="" 'q="" javascript="" variable'="" script="" +="@" "="" var="" return_a="xor_str(" "pipiscrew"");"="" var="" return_b="xor_str(q.toString());" convert="" js="" json="" object="" to="" string="" var="" arr="new" array();="" instantiate="" a="" js="" array="" arr.push(return_a);="" add="" item="" 0="" arr.push(return_b);="" add="" item="" 1="" arr;="" plain="" as="" is="" -="" outputs="" the="" variable="" to="" 'c#="" result'="" ";="" body="" main="" code="" object="" result="Microsoft.JScript.Eval.JScriptEvaluate(script," microsoft.jscript.vsa.vsaengine.createengine());="" if="" (result.gettype().name="=" "concatstring"="" ||="" result.gettype().name="=" "string")="" {="" messagebox.show(result.tostring());="" }="" else="" if="" (result.gettype().name="=" "arrayobject")="" {="" arrayobject="" obj="Result" as="" arrayobject;="" for="" (int="" i="0;" i=""></str.length;++i)>< int.parse(obj.length.tostring());="" i++)="" {="" console.writeline(obj[i]);="" }="" }="" else="" {="" messagebox.show("type="" is="" "="" +="" result.gettype().name);="" }="" }="" catch="" (exception="" ex)="" {="" messagebox.show(ex.message="" +="" ex.stacktrace);="" }="" }="" public="" string="" tojson(object="" obj)="" {="" javascriptserializer="" serializer="new" javascriptserializer();="" return="" serializer.serialize(obj);="" }="" }="" }="" ```=""  =""  ="">

## Simple equation

```js
string exp = "(1+6)*5/(7-4)";

Microsoft.JScript.Vsa.VsaEngine ve = Microsoft.JScript.Vsa.VsaEngine.CreateEngine();
double result = (double)Microsoft.JScript.Eval.JScriptEvaluate(exp, ve);

//result
Console.WriteLine(result);
```

origin - http://www.pipiscrew.com/?p=3469 net-js-evaluate