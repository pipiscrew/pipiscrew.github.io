---
title: Simple HTML DOM Parser
author: PipisCrew
date: 2019-10-30
categories: [php]
toc: true
---

[http://simplehtmldom.sourceforge.net/](http://simplehtmldom.sourceforge.net/)
https://simplehtmldom.sourceforge.io/manual_api.htm

## select with multiple css

```js
//when 
[test](g.com)

//parse 
$html->find('a.jobLink.jobInfoItem.jobTitle', 0)->innertext; //gives test
$html->find('a.jobLink.jobInfoItem.jobTitle', 0)->href;
```

## select element then class

```js
//when
<div class="snapshot-item"><i class="fa fa-building-o">test*

//parse
$html->find('div.snapshot-item fa-building-o', 0)->innertext; //gives test;
```

## select element then element

```js
//when
<div class="snapshot-item"><i class="fa fa-building-o">test*[LABEL](#)

//parse
$html->find('div.snapshot-item a', 0)->plaintext; //gives LABEL
```

## check if exists

```js
//when
<li class="next">[test](g.com)</li>

//parse
$h = $html->find('li.next>a', 0);

if ($h != null ) {
    echo $html->find('li.next>a', 0)->href
}
```

## use of prev_sibling / hasAttribute / getAttribute

```js
foreach($html->find('div.-item.-job') as $article) {

	$g = $article->prev_sibling();

	if ($g!=null)
		if ($g->hasAttribute("class"))
			if ($g->getAttribute("class") == "secondary-job-results-identifier" )
				break;
	.
	.
}
```

## get elements

```js
// Create DOM from URL or file
$html = file_get_html('http://www.google.com/');

// Find all images 
foreach($html->find('img') as $element) 
       echo $element->src . '  
';

// Find all links 
foreach($html->find('a') as $element) 
       echo $element->href . '  
';
```

## modify elements

```js
// Create DOM from string
$html = str_get_html('<div id="hello">Hello</div><div id="world">World</div>');

$html->find('div', 1)->class = 'bar';

$html->find('div[id=hello]', 0)->innertext = 'foo';

echo $html; // Output: <div id="hello">foo</div><div id="world" class="bar">World</div>
```

## extracting elements

```js
// Create DOM from URL
$html = file_get_html('http://slashdot.org/');

// Find all article blocks
foreach($html->find('div.article') as $article) {
    $item['title']     = $article->find('div.title', 0)->plaintext;
    $item['intro']    = $article->find('div.intro', 0)->plaintext;
    $item['details'] = $article->find('div.details', 0)->plaintext;
    $articles[] = $item;
}

print_r($articles);
```

In some page, SSL no working ?? - [https://stackoverflow.com/a/12446906/1320686](https://stackoverflow.com/a/12446906/1320686)

DOM Parser for PHP7 - [https://github.com/paquettg/php-html-parser](https://github.com/paquettg/php-html-parser)

PHP built-in - [https://www.tutorialspoint.com/php/php_dom_parser_example.htm](https://www.tutorialspoint.com/php/php_dom_parser_example.htm)</i></div></i></div>

origin - http://www.pipiscrew.com/?p=3057 php-simple-html-dom-parser