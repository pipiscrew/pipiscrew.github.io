---
title: o[asp.net] Repeater Example w/ ItemDatabound
author: PipisCrew
date: 2015-10-16
categories: [sql,.net,asp.net,linq]
toc: true
---

```js

    private long itemCount { get; set; }

    void Page_Load(Object Sender, EventArgs e)
    {
        WebApplication1.DataClasses1DataContext db = new WebApplication1.DataClasses1DataContext();

        var d = from p in db.customers select p;

        //Get the count of items in the data source. Subtract 1 for 0 based index.
        itemCount = d.Count() - 1;

        cdcatalog.DataSource = d;
        cdcatalog.DataBind();
    }

    protected void R1_ItemDataBound(object source, RepeaterItemEventArgs e)
    {
            // This event is raised for the header, the footer, separators, and items.

            // Execute the following logic for Items and Alternating Items.
            if (e.Item.ItemType == ListItemType.Item || e.Item.ItemType == ListItemType.AlternatingItem)
            {
                System.Diagnostics.Debug.WriteLine((e.Item.DataItem as WebApplication1.customer).cust_name);

                var x = (HtmlGenericControl) e.Item.FindControl("cust_namee");
                x.ID = "cust_namee" + e.Item.ItemIndex.ToString();
                x.InnerHtml = "test" ;

                //x.Attributes["css"] = "btn-primary";
                //or
                //x.Attributes.Add("class","TabPanelTabbedSelected");
                //or
                x.Attributes["class"] = "myCssClass3";

        	//If the item index is not = to the item count of the datasource - 1
                if (e.Item.ItemIndex != itemCount)
                   System.Diagnostics.Debug.WriteLine(itemCount);
            }
        }

```

```js
    <asp:Repeater id="cdcatalog" OnItemDataBound="R1_ItemDataBound" runat="server">
         <ItemTemplate>
            <li>

                <div id='cust_namee' clientidmode="static" runat="server" ></div>

            </li>
        </ItemTemplate>
    </asp:Repeater>

//ouputs HTML
<li>                
	<div id="cust_namee0" class="myCssClass3">test</div>
</li>

<li>
	<div id="cust_namee1" class="myCssClass3">test</div>
</li>

<li>
	<div id="cust_namee2" class="myCssClass3">test</div>
</li>
```

origin - http://www.pipiscrew.com/?p=2228 asp-net-repeater-example-w-itemdatabound