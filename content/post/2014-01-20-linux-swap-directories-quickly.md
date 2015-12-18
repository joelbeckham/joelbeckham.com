---
title: Linux swap directories quickly
author: jbeckham
layout: post
date: 2014-01-20
url: /2014/01/linux-swap-directories-quickly/
cudazi_post_settings:
  - default
categories:
  - Linux
---
If you&#8217;re hopping back and forth between say /etc/apache2 and /var/log/apache2. From /etc/apache2 type:

<pre>pushd /var/log/apache2</pre>

&nbsp;

This pushes /etc/apache2 on the directory stack and then cd&#8217;s to /var/log/apache2. Now to go back, just type:

<pre>pushd</pre>

&nbsp;

This swaps the current directory and the directory on the top of the stack. pushd again and you&#8217;re back to /var/log/apache2.