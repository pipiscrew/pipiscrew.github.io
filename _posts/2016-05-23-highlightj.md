---
title: highlight.js
author: PipisCrew
date: 2016-05-23
categories: [js,css]
toc: true
---

Syntax highlighting for the Web

```js(https://highlightjs.org/)

The bare minimum for using highlight.js on a web page is linking to the library along with one of the styles and calling **initHighlightingOnLoad**:

```js

hljs.initHighlightingOnLoad();

<style>
	code {font-size: 1.2em;}
</style>

        private void fill_x()
        {
            try
            {
                x.DataSource = null;
                DataTable dT = General.Conne.GetDATATABLE("select x,y from x_table order by x,y");
                DataRow dR = dT.NewRow();
                dR[0] = 0;
                dR[1] = "";
                dT.Rows.InsertAt(dR, 0);
                txtX_ID.DataSource = dT;
                txtX_ID.DisplayMember = "x_name";
                txtX_ID.ValueMember = "rec_id";
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "x", MessageBoxButtons.OK, MessageBoxIcon.Exclamation);
            }
        }

```

origin - http://www.pipiscrew.com/?p=5590 highlight-js