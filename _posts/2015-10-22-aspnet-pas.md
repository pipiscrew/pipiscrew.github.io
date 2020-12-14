---
title: o[asp.net] pass selected html_radio_button to code
author: PipisCrew
date: 2015-10-22
categories: [asp.net]
toc: true
---

```js
//html
<asp:HiddenField ID="hidden_BankDeposit_selected" ClientIDMode="Static" runat="server" />
<input name='btSelectItem' id='btSelectItem' onclick='set_selected_bank(this.id);' value='test1' type='radio'>
<input name='btSelectItem' id='btSelectItem' onclick='set_selected_bank(this.id);' value='test2' type='radio'>

//code
Comments += "\r\n" + this.hidden_BankDeposit_selected.Value;

//js
function set_selected_bank(id) {
    console.log(id);
    $("#hidden_BankDeposit_selected").val($("#"+id).val());
}
```

origin - http://www.pipiscrew.com/?p=2260 asp-net-pass-selected-html_radio_button-to-code