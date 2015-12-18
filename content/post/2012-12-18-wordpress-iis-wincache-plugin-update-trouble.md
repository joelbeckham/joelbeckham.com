---
title: WordPress + IIS + Wincache = plugin update trouble
author: jbeckham
layout: post
date: 2012-12-18
url: /2012/12/wordpress-iis-wincache-plugin-update-trouble/
categories:
  - Dev
tags:
  - Wordpress
---
A while ago, we started having trouble updating our wordpress plugins (and wordpress itself). Updating a plugin would fail with a &#8220;Could not remove the old plugin&#8221;. The plugin directory is there, but empty, and strangely cannot be deleted. We&#8217;ve found that restarting the app pool seems to resolve everything, even allowing the auto-update to work correctly.

We finally found the root cause. It&#8217;s a [known issue][1] with wordpress and the version (1.1.630.0) of wincache we&#8217;re using. Updating to the latest development build (1.2.1209) seems to have resolved the issue.

 [1]: http://wordpress.org/support/topic/wordpress-on-iis-7-plugin-update-problem?replies=33