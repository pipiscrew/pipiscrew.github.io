---
title: Add Background Color (Highlight) Option in WordPress Editor TinyMCE
author: PipisCrew
date: 2018-05-23
categories: [wordpress]
toc: true
---

add this to functions.php 

```js
//src - https://gist.github.com/thierrypigot/7fe4b3e40735d4b9a3ca
<?php
/* Hook to init */
add_action( 'init', 'tp_editor_background_color' );

/**
 * Add TinyMCE Button
 */
function tp_editor_background_color()
{
	/* Add the button/option in second row */
	add_filter( 'mce_buttons_2', 'tp_editor_background_color_button', 1, 2 ); // 2nd row
}

/**
 * Modify 2nd Row in TinyMCE and Add Background Color After Text Color Option
 */
function tp_editor_background_color_button( $buttons, $id )
{
	/* Only add this for content editor, you can remove this line to activate in all editor instance */
	if ( 'content' != $id )
		return $buttons;
	/* Add the button/option after 4th item */
	array_splice( $buttons, 4, 0, 'backcolor' );
	return $buttons;
}
```

origin - http://www.pipiscrew.com/?p=13747 add-background-color-highlight-option-in-wordpress-editor-tinymce