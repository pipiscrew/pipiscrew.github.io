---
title: Javascript for ASP.Net Client Side Validation
author: PipisCrew
date: 2016-04-21
categories: [js,asp.net]
toc: true
---

[http://smsohan.com/blog/2008/05/11/pageclientvalidate-use-this-method-from/](http://smsohan.com/blog/2008/05/11/pageclientvalidate-use-this-method-from/)

In a typical ASP.Net web form, we have a few controls and also validators associated with the controls. The most common validators are used for Required Field validation, Type validation, Regular Expression validation and so on.

When we want to logically group the validators in a web form, we apply the same value for ValidationGroup property on the controls of a group and in this way, we create a logical division among our controls and the validation. This may be important, if we want to validate only a subset of all the controls on a form when a button is clicked and do not want to validate all the controls on that form.

If we choose to use the client side validation, then the validation takes place before the post back occurs. This works fine unless you want to validate two distinct groups on a single button click, because a button can only specify a single value for ValidationGroup.

So, on a situation like this or when you actually want to invoke the client side validation using Javascript, you can make use of the following code to invoke the validation on controls belonging to a particular validation group -

```js
//test.js
Page_ClientValidate('testGroup');

//test.aspx
<form id="form1" runat="server">
    Your name:  

    <asp:textbox runat="server" id="txtName"></asp:textbox>
    <asp:requiredfieldvalidator runat="server" validationgroup="testGroup" id="reqName" controltovalidate="txtName" errormessage="Please enter your name!"></asp:requiredfieldvalidator>

    <asp:button runat="server" id="btnSubmitForm" text="Ok"></asp:button>
</form>
```

If, the result of validation of the controls in the ValidationGroup turns out to be valid, this method will return a ‘true’ or otherwise a ‘false’.

So, with this method, you will be able to invoke the client side ASP.Net validation using Javascript.

origin - http://www.pipiscrew.com/?p=5034 javascript-for-asp-net-client-side-validation