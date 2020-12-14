---
title: o[asp.net] create an ashx handler
author: PipisCrew
date: 2016-02-16
categories: [asp.net]
toc: true
---

references
[https://gist.github.com/tufanbarisyildirim/6763661](https://gist.github.com/tufanbarisyildirim/6763661)
[http://stackoverflow.com/q/4495961](http://stackoverflow.com/q/4495961)

1-Create an empty web application
2-RClick Project > Add New Item > WebForm (delete .designer + .cs files, hold only aspx)
3-RClick Project > Add New Item > Generic Handler

We have a webform into an aspx file. User with the selectbox can choose GET or POST.

![snap084](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap084.png)

```js
//WebForm1.aspx
<%@ Page Language="C#" EnableViewState="false" AutoEventWireup="true" %>

//void Button1_Click(Object sender, EventArgs e)
//{
//    Label1.Text = "Clicked at " + DateTime.Now.ToString();
//}

        $(function () {

            $('#frm').submit(function (e) {
                e.preventDefault();

                var postData = $(this).serializeArray();
                var formURL = $(this).attr("action");

                $.ajax(
                {
                    url: formURL,
                    type: $("#post_type").val(),
                    data: postData,
                    datatype: "json",
                    success: function (data, textStatus, jqXHR) {
                        $("#res_html").html(data);
                    },
                    error: function (jqXHR, textStatus, errorThrown) {
                        alert("ERROR - connection error");
                    }
                });
            });

        });

    <form id="frm" action="w.ashx" runat="server">
        <div>
            <input name="page" value="offers">  

            <input name="name" value="PipisCrew">  

            <input name="Blood Type" value="A-">  

            <input name="Married" value="No">  

            <select id="post_type">
                <option>GET
                <option>POST
            </select>  

            <button type="submit">SUBMIT</button>

        </div>
    </form>

    <div id="res_html" style="background-color:blue;color:white;"></div>

```

form submission intercepted by jQ at line 20^. When user selects GET at combo, make an AJAX GET call to ashx which return the result back to div line 63.  :

![snap085](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap085.png)

```js
//w.ashx
using System;
using System.Collections.Generic;
using System.Collections.Specialized;
using System.Linq;
using System.Web;

namespace WebApplicationASHX
{
    public class w : IHttpHandler
    {

        public void ProcessRequest(HttpContext context)
        {

            //Response.ContentType = "text/html";
            //context.Response.Write("Hello World");

            if (Request.RequestType == "GET")
            {
                foreach (String key in Request.QueryString.AllKeys)
                {
                    Response.Write(key + " : " + Request.QueryString[key] + "  
");
                }
            }
            else if (context.Request.RequestType == "POST")
            {
                string[] keys = context.Request.Form.AllKeys;

                validate_post(keys);

                for (int i = 0; i < keys.length;="" i++)="" {="" response.write(keys[i]="" +="" ":="" "="" +="" request.form[keys[i]]="" +=""></br>");
                }
            }
        }

        internal void offers(string[] keys)
        {

        }

        internal void validate_post(string[] keys)
        {
            try
            {
                if (keys.Contains("your_key"){
                    Request.Form["your_key"];
                } else 
                	kick_user();
            }
            catch (Exception x)
            {
                Response.Write(x.Message);
                Response.End();
            }
        }

        internal void kick_user()
        {
            //kick with 500
            Response.StatusCode = 500;
            Response.ContentType = "text/plain";
            Response.Write("Server internal error");
            Response.End();
        }

        //
        HttpRequest Request { get { return HttpContext.Current.Request; } }

        HttpResponse Response { get { return HttpContext.Current.Response; } }

        public bool IsReusable { get { return false; } }
    }
}
```

when user make a POST, falls to **validate_post** method, which asking for specific key that not exists and response the error. :

![snap086](https://www.pipiscrew.com/wp-content/uploads/2016/02/snap086.png)

origin - http://www.pipiscrew.com/?p=3856 asp-net-create-an-ashx-handler