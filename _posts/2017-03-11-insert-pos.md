---
title: Insert post to wordpress from your custom PHP code
author: PipisCrew
date: 2017-03-11
categories: [php,wordpress]
toc: true
---

reference - https://developer.wordpress.org/reference/functions/wp_insert_post/

```js
//https://wordpress.org/support/topic/insert-post-from-php-script/page/2/#post-8492728
<?php

ini_set('display_errors', 1);
error_reporting(E_ALL);

require_once('wp-load.php');

// Create post object
$my_post = array(
	'post_title' => 'qwe',
	'post_content' => wp_strip_all_tags($content),
	'post_status' => 'publish',
	'post_author' => '1',
	'post_category' => array( 1,2 )
);

wp_insert_post( $my_post );

?>
```

### Bulk insert from a category to another

```js
//http://wordpress.stackexchange.com/a/231822
defined('WP_USE_THEMES') || define('WP_USE_THEMES', false);
require_once('wp-load.php');
global $wpdb;
$sql = "SELECT * FROM {$wpdb->prefix}newposts";
$result = $wpdb->get_results($sql);  
foreach ( $result as $row ) :;
    $row = (array) $row;
    $post = array(
        'post_title' => $row['post_title'],
        'post_content' => $row['post_content'],
        'post_date' => $row['post_date'],
        'post_date_gmt' => $row['post_date_gmt'],
        'post_status' => 'publish',
        'post_author' => 1,
        'post_category' => array(1)
    );
    wp_insert_post( $post );
    echo "inserted post {$row['post_title']}";
    echo "  
";
endforeach;
```

snippet with login form - https://gist.github.com/pipiscrew/89576983967179fd1c23203fcf46ec40

#wordpress

origin - http://www.pipiscrew.com/?p=6753 insert-post-to-wordpress-from-your-custom-php-code