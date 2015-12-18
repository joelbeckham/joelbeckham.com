---
title: F12 Developer tools disabled in IE8
author: jbeckham
layout: post
date: 2012-02-10
url: /2012/02/f12-developer-tools-disabled-in-ie8/
categories:
  - Dev
tags:
  - IE
---
For some reason I couldn&#8217;t pull the up the F12 Developer tools in IE8. The menu item was grayed out. Here&#8217;s how I got them back:

  1. Start up gpedit.msc
  2. Go to **_Computer Configuration_** -> **_Administrative Templates_** -> **_Windows Components_** -> **_Internet Explorer_** -> **_Toolbars_**
  3. Right click on **_Turn off Developer Tools_** -> **_Edit_**
  4. I set it **_Disabled_**. You could try enabling then disabling it if just disabling it doesn&#8217;t work.

&#160;

[<img style="background-image: none; border-right-width: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="2012-02-10_094108" border="0" alt="2012-02-10_094108" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-10_094108_thumb.gif?resize=576%2C278" data-recalc-dims="1" />][1]

 [1]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-10_094108.gif