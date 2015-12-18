---
title: 'Triggering xdebug from PHPStorm's REST client'
author: jbeckham
layout: post
date: 2014-01-09
url: /2014/01/triggering-xdebug-from-phpstorms-rest-client/
cudazi_post_settings:
  - default
categories:
  - PHP
---
If you want to trigger and xdebug session from PHPStorm's REST client (or anywhere else for that matter), you can set the debug cookie manually. Add a new Request header:

  * Name: Cookie
  * Value: XDEBUG_SESSION=PHPSTORM

<a href="http://www.joelbeckham.com/blog/2014/01/09/triggering-xdebug-from-phpstorms-rest-client/phpstorm-xdebug-cookie/" rel="attachment wp-att-485"><img class="alignnone size-full wp-image-485" alt="phpstorm-xdebug-cookie" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2014/01/phpstorm-xdebug-cookie.png?resize=473%2C154" data-recalc-dims="1" /></a>

The value to use for XDEBUG_SESSION can be set in php.ini under xdebug.idekey

&nbsp;
