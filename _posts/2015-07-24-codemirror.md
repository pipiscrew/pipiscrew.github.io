---
title: CodeMirror
author: PipisCrew
date: 2015-07-24
categories: []
toc: true
---

reference :
[http://codemirror.net/](http://codemirror.net/)
[http://github.com/codemirror/CodeMirror/](http://github.com/codemirror/CodeMirror/)

similar - [http://ace.c9.io/](http://ace.c9.io/)

all referenced files include on github zip^ 

```js

			$(function() {

				//button click
				$('#btn').on('click', function(e) {
					console.log(editor.getValue()); //get plain text
					//clear
					editor.setValue("");
					editor.clearHistory();
					//clear undo+redo
					console.log(editor.getValue()); //verify is cleared
				});

			});

## Demo

		<button id="btn">
			Read code & reset
		</button>

<form><textarea id="code" name="code">

## Demo

	function Grid(width, height) {
	  this.width = width;
	  this.height = height;
	  this.cells = new Array(width * height);
	}
</textarea></form>

//on page render

      var editor = CodeMirror.fromTextArea(document.getElementById("code"), {
      lineNumbers: true,
      styleActiveLine: true,
      matchBrackets: true
    });

```

## using on bootstrap v3.x modal

```js

origin - http://www.pipiscrew.com/?p=3235 js-codemirror