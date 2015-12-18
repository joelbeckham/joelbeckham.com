---
title: Google Maps API v3 InfoWindow missing corners
author: jbeckham
layout: post
date: 2011-08-20
url: /2011/08/google-maps-api-v3-infowindow-missing-corners/
categories:
  - Dev
---
[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="image" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/image_thumb.png?resize=220%2C174" alt="image" border="0" data-recalc-dims="1" />][1]

I ran into this issue embedding a map into a wordpress site using the default wordpress theme. This CSS rule is the culprit::

<pre class="csharpcode" style="width: 577px; height: 147px;">#content img {
  margin: 0;
  height: auto;
  max-width: 640px;
  width: auto;
}</pre>

max-width is overriding the maps img max-width of none. This can be fixed with:

<pre class="csharpcode">#map_canvas img { max-width: none; }</pre>

&nbsp;

Or if you can’t modify the style sheets, you can do it through jQuery:

<pre class="csharpcode">$(<span class="str">"&lt;style type='text/css'&gt; #map_canvas img{ max-width: none; } &lt;/style&gt;"</span>).appendTo(<span class="str">"head"</span>);</pre>

 [1]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/image.png