---
title: from wenzhixin bootstrap-table to angular akveo ng2-smart-table
author: PipisCrew
date: 2019-07-06
categories: [angular,va]
toc: true
---

installation - https://github.com/akveo/ng2-smart-table#installation
documentation - https://akveo.github.io/ng2-smart-table/#/documentation
example - https://akveo.github.io/ng2-smart-table

*   server side pagination

*   search

*   column formatter

* * *

## Installation

go to angular root of project ( aka where <span style="font-size: large; background-color: #ffff00;">package.json</span> exists)

execute :

<span style="text-decoration: line-through;">npm install --save rxjs-compat hxxps://github.com/akveo/ng2-smart-table/issues/270#issuecomment-445528965</span>

```js

npm install --save ng2-completer
npm install --save ng2-smart-table

```

this will download & import the library to <span style="background-color: #ffff00;">root_project\node_modules</span>

![](https://i.imgur.com/XqRrh6b.png)

[fsevents reference](https://stackoverflow.com/a/40464936)

we going to VSCode to parent **.module.ts** of the needed component and paste :
```js
import { HttpClientModule } from '@angular/common/http'; 
import { Ng2SmartTableModule } from 'ng2-smart-table';

@NgModule({
  declarations: [AppComponent],
  imports: [
    HttpClientModule,
    Ng2SmartTableModule
  ]
})

```

we going to the needed **.component.html** and paste the :
```js
//test
<ng2-smart-table [settings]="settings" [="" source="" ]="source"></ng2-smart-table>
```

we going to the needed **.component.ts** and paste the :
```js
import { HttpClient } from '@angular/common/http';
import { ServerDataSource } from 'ng2-smart-table';

export class PipisCrewTestComponent {

  settings = {
    columns: {
      id: {
        title: 'ID',
      },
      albumId: {
        title: 'App',
      },
      title: {
        title: 'Developer',
      },
      url: {
        title: 'Url',
      },
    },
  };

  source: ServerDataSource;

  constructor(http: HttpClient) {
    this.source = new ServerDataSource(http, { endPoint: 'https://jsonplaceholder.typicode.com/photos' });
  }
```

* * *

## Table parameters

```js
  settings = {
    pager : {perPage:50},                            //pagination – rows per page
    hideSubHeader: true,                             //hide header searchboxes for search (filters)
    actions:{add:false, edit:false, delete:false},   //hide first column having ADD DELETE anchors
    attr:{class:"table table-hover table-striped"},  //use bootstrap zebra style
    columns: {
      id: {
        title: 'ID',
      },
      albumId: {
        title: 'App',
      },
      title: {
        title: 'Developer',
      },
      url: {
        title: 'Url',
      },
    },
  };
```

example of **valuePrepareFunction**
```js
  settings = {
    hideSubHeader: true,
    actions:{add:false, edit:false, delete:false},
    attr:{class:"table table-hover table-striped"},
    columns: {
      id: {
        title: 'ID',
        valuePrepareFunction: (value) => {
          if (value == 1)
            return 'pipiscrew';
          else 
            return value;
        }
      },
      albumId: {
        title: 'App',
      },
      title: {
        title: 'Developer',
      },
      url: {
        title: 'Url',
      },
    },
  };
```

![](https://i.imgur.com/V5QGia3.png)

accessing other **row fields** via **valuePrepareFunction**

```js
//src - https://github.com/akveo/ng2-smart-table/issues/394

albumId: {
	title: 'App',
	valuePrepareFunction: (cell, row) => {
		console.log(row.id);
	}
},
```

when we like to **render the value** as **HTML**, we have to set the **column type** to html. [reference](https://github.com/akveo/ng2-smart-table/issues/315#issuecomment-296383697)
```js
/*  settings = {
    hideSubHeader: true,
    actions:{add:false, edit:false, delete:false},
    attr:{class:"table table-hover table-striped"},
    columns: {*/
      id: {
        title: 'ID',
        type: "html",
        valuePrepareFunction: (value) => {
          if (value == 1)
            return '<i class="fab fa-accessible-icon">*';
          else 
            return value;
        }
      },
/*      albumId: {
        title: 'App',
      },
      title: {
        title: 'Developer',
      },
      url: {
        title: 'Url',
      },
    },
  };*/
```

the **renderComponent**, is responsible for rendering the cell content while in **view mode**, basic example with **routerLink**

```js
//src - https://stackblitz.com/edit/angular-bqsxidq-omgedw?file=src/app/users/userlist/userlist.component.ts or https://github.com/varmamkm/angular-route-resolver-ng2-smart-table
  settings = {
    actions: false,
    columns: {
      username: {
        title: 'User Name',
        type: 'custom',
        renderComponent: UserlistRowRenderComponent
      },
      name: { title: 'Full Name' },
      email: { title: 'Email' }
    }
  };

//userlistrowrender.component.ts
// src - https://stackblitz.com/edit/angular-bqsxidq-omgedw?file=src/app/users/userlist/userlistrowrender.component.ts
import { Input, Component, OnInit } from '@angular/core';
import { ViewCell } from 'ng2-smart-table';

@Component({
  template: `[{{ username }}]()`,
})

export class UserlistRowRenderComponent implements ViewCell, OnInit {
  public username: string;
  public userId: number;

  @Input()
  public value: string;

  @Input()
  rowData: any;

  ngOnInit() {
    this.username = this.value;
    this.userId= this.rowData.id;
  }
}
```

line 21 - use of variables (35,36)

use of **renderComponent** with dropdown button and **EventEmitter** to raise event to parent component
```js
/*
https://github.com/pipiscrew/angular2_small_prjs/tree/master/ng2-smart-table-renderer_EventEmitter

https://github.com/pipiscrew/angular2_small_prjs/tree/master/ng2-smart-table-renderer_MultipleActions
*/
```

* * *

## Turn GET calls to POST

![](https://i.imgur.com/enxtTzr.png)

Create a new class extending ServerDataSource (ng2-smart-table\lib\lib\data-source\server\server.data-source.d.ts)

```js
//greets to aefox - https://github.com/akveo/ng2-smart-table/issues/828
//postserverdatasource.ts
import { Observable } from 'rxjs/internal/Observable';
import { ServerDataSource } from 'ng2-smart-table';

export class PostServerDataSource extends ServerDataSource {

    protected requestElements(): Observable<any> {
        let httpParams = this.createRequesParams();
        return this.http.post(this.conf.endPoint, httpParams, { observe: 'response' });
    }

}
```

then to **.component.ts** use instead ServerDataSource :

```js
  constructor(http: HttpClient) {

    //this.source = new ServerDataSource(http, { endPoint: 'https://jsonplaceholder.typicode.com/photos' });
    this.source = new PostServerDataSource(http, { endPoint: 'http://localhost:8000' });

  }
```

* * *

## Change POST parameters key name

by default is with underscore :

![](https://i.imgur.com/1SqRheV.png)

the ng2-smart-table **ServerDataSource** class by default accepts **server-source.conf** parameters (data-source\server\server-source.conf.d.ts) on constructor, enable us to set the key names :

```js
//before - this.source = new PostServerDataSource(http, { endPoint: this.conf.endPoint});
this.source = new PostServerDataSource(http, { endPoint: this.conf.endPoint, pagerPageKey: "page", pagerLimitKey: "limit", filterFieldKey : "#field#" });
```

![](https://i.imgur.com/Qd4BHdT.png)

* * *

ref - when client side - The [filterFunction](https://stackoverflow.com/a/53463610) used by columns searchboxes for search " How to search column after applying valuePrepareFunction()”

* * *

## Filter field with select

![](https://i.imgur.com/w4goAai.png)

```js
      Roles: {
        title: 'Role',filter: {
          type: 'list',
          config: {
            selectText: '-none-',
            list: [
              {value: '1', title:'admin'},
              {value: '2', title:'restricted'},
              {value: '3', title:'entry'},
              {value: '4', title:'report'},
            ],
          }
        }
      }
```

## Disable filter field

```js
      car_type: {
        title: 'TestField', 
        filter: false
      },
```

* * *

templates/frameworks from akveo team :
[ngx-admin](https://akveo.github.io/ngx-admin/)
[UI Kitten](https://akveo.github.io/react-native-ui-kitten/)
[Eva Design System](https://eva.design/)

--

[wenzhixin.bootstrap-table - usage without any framework](https://github.com/wenzhixin/bootstrap-table/issues/4364)</any></i>

origin - https://www.pipiscrew.com/?p=15033 from-wenzhixin-bootstrap-table-to-angular-akveo-ng2-smart-table