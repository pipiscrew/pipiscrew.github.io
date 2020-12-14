---
title: The famous XML-RPC
author: PipisCrew
date: 2017-03-03
categories: [wordpress]
toc: true
---

Is a list of servers that WordPress notifies every time you publish a new blog post on your website. By sending an XML-RPC ping when you publish new material or update older blog posts, you can get indexed in the different search engines. Can found under Settings > Writing > Update Services

ref -
https://codex.wordpress.org/Update_Services
http://phppot.com/wordpress/wordpress-xml-rpc-update-services-to-ping/
http://www.blogsnow.com/ping
https://gist.github.com/chopdeniks/57fc812aa7ba05f4016998ae2f4342a5

### What actually does when you add/edit a post ?

ref - https://books.google.com/books?id=lwyDNLIEkfkC&pg=PT279&lpg=PT279
All it does is alert the search engines that there is new content to look at. The search engines can find the new post and use any information from the  post. The category and tag are important.

Here is dump of a call to XML-RPC service (using Wordpress v4.7.2) :
```js
//sample
<?xml version="1.0"?>
<methodCall>
<methodName>weblogUpdates.ping</methodName>
<params>
<param><value><string>PipisCrew Official Homepage</string></value></param>
<param><value><string>https://www.pipiscrew.com/</string></value></param>
</params></methodCall>
```

**Conclusion :** 
When you add/edit a post, wordpress just call the ‘ping service’ to index your site, the call is not specific for the current post, is independent, as result you can call it from your custom CMS, there is no requirement to be Wordpress.

• Some of those websites list your blog in their recently updated blog list. (ex http://weblogs.com/)
• Blog search engines like Google Blog Search, Yahoo Search Blog, etc… also crawl and index your blog which in turn send additional traffic.

You  can manual submit your site to ‘wordpress ping service’ - http://pingomatic.com/  (the wordpress default is http://rpc.pingomatic.com/)

More info - http://tldp.org/HOWTO/XML-RPC-HOWTO/xmlrpc-howto-intro.html#xmlrpc-howto-spec

origin - http://www.pipiscrew.com/?p=6990 the-famous-xml-rpc