---
title: Telerik.Kendo UI Grid - kendoDropDownList filter - add name + id values, then filter by ID
author: PipisCrew
date: 2020-09-08
categories: [js,.net]
toc: true
---

What if you want to display a text value to a grid to column and instead search by it Id through Filter predefined combo ?

The filter added to column :

```js
columns: [
	{
		field: "Player",
		title: "Player",
		headerTemplate: '<span title="Player">Player</span>',
		attributes: { "class": "col-show-tooltip" },
		filterable: {
			ui: playerFilter,
			operators: { string: { eq: "Is equal to" } }
		}
	}
]
```

the function called when going to show the filter panel

```js
function playerFilter(element) {
	element.kendoDropDownList({
		dataTextField: "Name",
		dataValueField: "Id",
		dataSource: {
			serverFiltering: true,
			schema: {
				data: "Data",
				type: "json"
			},
			transport: {
				read: {
					url: "/api//GetFilterPlayers",
					contentType: "application/json",
					dataType: "json",
					type: "POST"
				}
			}
		},
		optionLabel: "-Select Value-"
	});
}
```

the function fills the kendoDropDownList filter, returns a keypair array

```js
public DataSourceResult GetFilterPlayers(FilterRequest req)
{
	return this.cx.Players
		.OrderBy(x => x.FullName)
		.Select(x => new
		{
			Name = x.FullName,
			Id = x.PlayerId
		})
	   .ToDataSourceResult(1000, 0, null, null);
}
```

when search (filter) button clicked, call the service to fill the grid (generic for all fill grid actions)

```js
public DataSourceResult GetGridPlayers(DataSourceRequest req) {
//we revert the request filter field name to PlayerId, otherwise will search on text field Player
if (req.Filter != null && req.Filter.Filters.Any(x => x.Field == "Player"))
{
	var playerSearchFilter = req.Filter.Filters.First(x => x.Field == "Player");
	playerSearchFilter.Field = "PlayerId";
}

return this.cx.Players.ToDataSourceResult(req.Take, req.Skip, req.Sort, req.Filter);
}
```

ref - https://webfed.gitee.io/fs/book/kendo-ui/api/javascript/ui/dropdownlist

origin - https://www.pipiscrew.com/?p=19049 telerik-kendo-ui-grid-kendodropdownlist-filter-add-name-id-values-then-filter-by-id