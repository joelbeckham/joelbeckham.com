---
title: '<head runat="server">'
author: jbeckham
layout: post
date: 2012-01-19
url: /2012/01/head-runatserver/
categories:
  - Dev
tags:
  - HTML
---
I just noticed that at some point all of my page titles became blank and the <title> tag in the markup was empty. The reason is because the <head> tag wasn&#8217;t marked as a server-side tag for ASP.NET, so it didn&#8217;t have access to update the <title> tag.