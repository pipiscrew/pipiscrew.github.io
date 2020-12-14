---
title: o[html] Google Custom Search
author: PipisCrew
date: 2015-08-02
categories: []
toc: true
---

Got a blogroll or a directory you want to make searchable? Here's a quick and easy way to create a search engine from the links on your web page.

[http://cse.google.com/cse/tools/create_onthefly](http://cse.google.com/cse/tools/create_onthefly)

* * *

> Create Crawlable, Link-Friendly AJAX Websites Using pushState()

[https://moz.com/blog/create-crawlable-link-friendly-ajax-websites-using-pushstate](https://moz.com/blog/create-crawlable-link-friendly-ajax-websites-using-pushstate)

```js
// We're using jQuery functions to make our lives loads easier
$('nav a').click(function(e) {
      url = $(this).attr("href");

      //This function would get content from the server and insert it into the id="content" element
      $.getJSON("content.php", {contentid : url},function (data) {
            $("#content").html(data);
      });

      //This is where we update the address bar with the 'url' parameter
      window.history.pushState('object', 'New Title', url);

      //This stops the browser from actually following the link
      e.preventDefault();
}
```

* * *

> SEO-Friendly URL Structure

[http://webdesign.tutsplus.com/articles/how-to-create-an-seo-friendly-url-structure--webdesign-9569](http://webdesign.tutsplus.com/articles/how-to-create-an-seo-friendly-url-structure--webdesign-9569)
[http://techterms.com/definition/friendly_url](http://techterms.com/definition/friendly_url)
[http://stackoverflow.com/a/8485137/1320686](http://stackoverflow.com/a/8485137/1320686)

#seo

origin - http://www.pipiscrew.com/?p=3268 html-google-custom-search