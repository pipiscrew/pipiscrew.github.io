---
title: Bookmarklet - Fill input fields, fire an event then click a button
author: PipisCrew
date: 2020-07-04
categories: [js]
toc: true
---

```js
javascript: {  document.getElementsByClassName('APassAttr')[0].value = 1; document.getElementById('CountryLocationAddress').value = 4020; document.getElementById('CountryLocationAddress').dispatchEvent(new Event('change')); document.getElementsByName('activityTime')[0].value = '00'; document.getElementById('companyAddress').value = 'Mesogeiwn'; document.getElementById('companyCity').value = 'Athens'; document.getElementById('save').click(); void(0) }
```

beautified :
```js
document.getElementsByClassName('APassAttr')[0].value = 1 //element selector by CLASS (returns an array, then grab the first)
document.getElementById('CountryLocationAddress').value = 4020; //select inputbox
document.getElementById('CountryLocationAddress').dispatchEvent(new Event('change')); //fire event - change
document.getElementsByName('activityTime')[0].value = '00'; //element selector by NAME (returns an array, then grab the first)
document.getElementById('companyAddress').value = 'Mesogeiwn'; //element selector by ID
document.getElementById('companyCity').value = 'Athens'; // set input value
document.getElementById('save').click(); //click button - submit form 
```

dispatch event - refs :
https://2ality.com/2013/06/triggering-events.html
https://gomakethings.com/custom-events-in-internet-explorer-with-vanilla-js/

click ref :
https://stackoverflow.com/a/3822931/1320686

bookmarklet ref :
https://stackoverflow.com/a/11301539/1320686

* * *

Open new tab and submit a form 
```js
javascript: (function() {
    var openWindow = window.open('');
    var url = window.document.URL.toString();
    var src = document.documentElement.innerHTML;
    var note = 'book';
    form = document.createElement('form');
    form.setAttribute('method', 'POST');
    form.setAttribute('action', 'https://www.tubeoffline.com/downloadFrom.php');
    form.setAttribute('onsubmit', 'Submit.disabled = true;return true;');
    srcPlaceholder = document.createElement('input');
    srcPlaceholder.setAttribute('name', 'src');
    srcPlaceholder.setAttribute('type', 'hidden');
    srcPlaceholder.setAttribute('value', src);
    form.appendChild(srcPlaceholder);
    urlPlaceholder = document.createElement('input');
    urlPlaceholder.setAttribute('name', 'url');
    urlPlaceholder.setAttribute('type', 'hidden');
    urlPlaceholder.setAttribute('value', url);
    form.appendChild(urlPlaceholder);
    notePlaceholder = document.createElement('input');
    notePlaceholder.setAttribute('name', 'note');
    notePlaceholder.setAttribute('type', 'hidden');
    notePlaceholder.setAttribute('value', note);
    form.appendChild(notePlaceholder);
    divPlaceholder = document.createElement('div');
    divPlaceholder.setAttribute('name', 'label');
    divPlaceholder.setAttribute('type', 'div');
    divPlaceholder.style.textAlign = 'center';
    divPlaceholder.style.fontWeight = 'bold';
    divPlaceholder.style.fontSize = '18px';
    divPlaceholder.style.fontFamily = 'arial';
    divPlaceholder.innerHTML = '  

Click the below button to Continue.  
If your download does not work, please send feedback so we fix it for you.  

';
    form.appendChild(divPlaceholder);
    btn = document.createElement('input');
    btn.setAttribute('name', 'Submit');
    btn.setAttribute('type', 'submit');
    btn.setAttribute('value', 'Go To TubeOffline download page >>');
    btn.style.fontSize = '24px';
    btn.style.fontWeight = 'bold';
    btn.style.color = '#FA8507';
    btn.style.width = '600px';
    btn.style.height = '100px';
    btn.style.display = 'table';
    btn.style.margin = '0 auto';
    btn.setAttribute('onclick', "this.value='Converting Video, Please wait...'");
    form.appendChild(btn);
    openWindow.document.body.appendChild(form)
})();
```

origin - https://www.pipiscrew.com/?p=16518 bookmarklet-fill-input-fields-fire-an-event-then-click-a-button