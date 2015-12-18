---
title: Compacting a dynamic VHD
author: jbeckham
layout: post
date: 2013-01-17
url: /2013/01/compacting-a-dynamic-vhd/
cudazi_post_settings:
  - default
categories:
  - Dev
---
Start Diskpart from the command prompt.

<pre>select vdisk file="&lt;path&gt;"</pre>

<pre>compact vdisk</pre>

&nbsp;