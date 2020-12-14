---
title: o[wordpress] Disable Post Revisions
author: PipisCrew
date: 2016-02-05
categories: [news,sql,wordpress]
toc: true
---

[https://codex.wordpress.org/Revisions](https://codex.wordpress.org/Revisions)

Alternately, the limit can be set in wp-config.php:

```js
define( 'WP_POST_REVISIONS', 3 );

WP_POST_REVISIONS:
-true (default), -1: store every revision
-false, 0: do not store any revisions (except the one autosave per post)
-(int) > 0: store that many revisions (+1 autosave) per post. Old revisions are automatically deleted.
```

or use the plugin
[https://el.wordpress.org/plugins/better-delete-revision/](https://el.wordpress.org/plugins/better-delete-revision/)

## Delete existing revisions

similar - [http://bacsoftwareconsulting.com/blog/index.php/web-programming/how-to-delete-and-limit-revisions-in-wordpress/](http://bacsoftwareconsulting.com/blog/index.php/web-programming/how-to-delete-and-limit-revisions-in-wordpress/)

```js
DELETE FROM wp_posts WHERE post_type = 'revision';
```

origin - http://www.pipiscrew.com/?p=3328 wordpress-disable-post-revisions