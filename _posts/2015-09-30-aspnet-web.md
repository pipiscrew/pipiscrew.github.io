---
title: o[asp.net] WebControls and HtmlControls
author: PipisCrew
date: 2015-09-30
categories: [asp.net]
toc: true
---

reference [http://odetocode.com/articles/348.aspx](http://odetocode.com/articles/348.aspx)

Server-based controls are the epitome of encapsulation. Developers can manipulate control objects 
programmatically using code to customize their appearance, provide data to display, and even react to 
events. The low-level HTML markup that these controls render is hidden away behind the scenes. 
Instead of forcing the developer to write raw HTML manually, the control objects render themselves to 
HTML just before the web server sends the page to the client. In this way, ASP.NET offers server controls 
as a way to abstract the low-level details of HTML and HTTP programming. 
Here’s a quick example with a standard HTML text box that you can define in an ASP.NET web page: 
```js<input type="text" id="myText" runat="server"> ```

With the addition of the runat="server" attribute, this static piece of HTML becomes a fully 
functional server-side control that you can manipulate in code. You can now work with events that it 
generates, set attributes, and bind it to a data source. 
For example, you can set the text of this box when the page first loads using the following code: 
 ```js
public class WebForm1 : System.Web.UI.Page
{
	protected void Page_Load(object sender, System.EventArgs e)
	{
		myText.Value = "Hello World";
	}
}
 ```

Technically, this code sets the Value property of an HtmlInputText object. The end result is that a 
string of text appears in a text box on the HTML page that’s rendered and sent to the client. 

* * *

## HTML CONTROLS VS. WEB CONTROLS 

When ASP.NET was first created, two schools of thought existed. Some ASP.NET developers were most 
interested in server-side controls that matched the existing set of HTML controls exactly. This approach 
allows you to create ASP.NET web-page interfaces in dedicated HTML editors, and it provides a quick 
migration path for existing ASP pages. However, another set of ASP.NET developers saw the promise of 
something more—rich server-side controls that didn’t just emulate individual HTML tags. These controls 
might render their interface from dozens of distinct HTML elements while still providing a simple object-
based interface to the programmer. Using this model, developers could work with programmable menus, 
calendars, data lists, validators, and so on.   

After some deliberation, Microsoft decided to provide both models. You’ve already seen an example of 
HTML server controls, which map directly to the basic set of HTML tags. Along with these are ASP.NET 
web controls, which provide a higher level of abstraction and more functionality. In most cases, you’ll use 
HTML server-side controls for backward compatibility and quick migration, and use web controls for new  projects  

ASP.NET web control tags always start with the prefix 
**asp:** 
 followed by the class name. For example, the 
following snippet creates a text box and a check box: 
```js
<asp:textbox id="myASPText" text="Hello ASP.NET TextBox" runat="server"></asp:textbox> 
<asp:checkbox id="myASPCheck" text="My CheckBox" runat="server"></asp:checkbox> 
```
Again, you can interact with these controls in your code, as follows: 

```js
myASPText.Text = "New text" 
myASPCheck.Text = "Check me!" 
```

Notice that the Value property you saw with the HTML control has been replaced with a Text property. The 
HtmlInputText.Value property was named to match the underlying value attribute in the HTML ```js<input>``` tag. 
However, web controls don’t place the same emphasis on correlating with HTML syntax, so the more 
descriptive property name Text is used instead.   

The ASP.NET family of web controls includes complex rendered controls (such as the Calendar and 
TreeView), along with more streamlined controls (such as TextBox, Label, and Button), which map closely 
to existing HTML tags. In the latter case, the HTML server-side control and the ASP.NET web control 
variants provide similar functionality, although the web controls tend to expose a more standardized, 
streamlined interface. This makes the web controls easy to learn, and it also means they’re a natural fit for 
Windows developers moving to the world of the Web, because many of the property names are similar to 
the corresponding Windows controls.

origin - http://www.pipiscrew.com/?p=2073 asp-net-webcontrols-and-htmlcontrols