---
title: WordPress Admin Alert
author: jbeckham
layout: post
date: 2012-04-25
url: /2012/04/wordpress-admin-alert/
categories:
  - Dev
tags:
  - Wordpress
---
If you want to show a message in the Admin area of wordpress, add the following to your functions.php of your theme:

<pre class="lang:php decode:true ">add_action( 'admin_notices', 'warning_method' );

function warning_method()
{
   echo '&lt;div&gt;Message here.&lt;/div&gt;';
}</pre>

&nbsp;