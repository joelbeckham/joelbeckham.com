---
title: jQuery DataTables causing slow script errors in Internet Explorer
author: jbeckham
layout: post
date: 2011-09-21
url: /2011/09/jquery-datatables-causing-slow-script-errors-in-internet-explorer/
categories:
  - Dev
tags:
  - jQuery
---
One of my pages gets a &quot;Stop running this script? A script on this page is causing Internet Explorer to run slowly. If it continues to run, your computer might become unresponsive.&quot;

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="ie_slow_script_error" border="0" alt="ie_slow_script_error" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/ie_slow_script_error_thumb.png?resize=336%2C153" data-recalc-dims="1" />][1]

Running the page through <a href="http://code.google.com/webtoolkit/speedtracer/get-started.html#downloading" target="_blank">Speed Tracer</a> in Chrome shows this:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_110622" border="0" alt="2011-09-21_110622" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_110622_thumb.gif?resize=401%2C383" data-recalc-dims="1" />][2]

DOMContentLoaded looks like it might be the problem. Drilling down into reveals that there are hundreds of DOM insertions and HTML parses:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_110654" border="0" alt="2011-09-21_110654" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_110654_thumb.gif?resize=275%2C281" data-recalc-dims="1" />][3]

&#160;

here is a lot of javascript on this page, but I suspect it might be the <a href="http://datatables.net/index" target="_blank">jQuery DataTables plugin</a>. Removing the plugin confirms my suspicion:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_113120" border="0" alt="2011-09-21_113120" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_113120_thumb.gif?resize=312%2C21" data-recalc-dims="1" />][4]

One thing that could be causing the DOM insertions is the DataTable’s fnRender function. The majority of the columns call this function to render the value as a percent and to highlight it in red if it is negative:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_110734" border="0" alt="2011-09-21_110734" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_110734_thumb.gif?resize=496%2C257" data-recalc-dims="1" />][5]

If the value is positive, it just appends a percent, but if it is negative, it’s adding a span tag with the new style:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_110748" border="0" alt="2011-09-21_110748" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_110748_thumb.gif?resize=419%2C126" data-recalc-dims="1" />][6]

I’m going to remove the special case for the negatives and just see if it speeds things up:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_112109" border="0" alt="2011-09-21_112109" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112109_thumb.gif?resize=309%2C76" data-recalc-dims="1" />][7]

That helped a little bit:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_112217" border="0" alt="2011-09-21_112217" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112217_thumb.gif?resize=336%2C19" data-recalc-dims="1" />][8]

Drilling down shows it removed all the DOM insertions, but there are still hundreds of Parse HTML’s:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_112250" border="0" alt="2011-09-21_112250" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112250_thumb.gif?resize=203%2C174" data-recalc-dims="1" />][9]

If I remove the render function completely:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_112422" border="0" alt="2011-09-21_112422" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112422_thumb.gif?resize=578%2C363" data-recalc-dims="1" />][10]

That cut the time in half:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_112532" border="0" alt="2011-09-21_112532" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112532_thumb.gif?resize=329%2C19" data-recalc-dims="1" />][11]

I think I will add the percent sign server side and add the negative style to the td element server side as well.

Trying a couple other things, I found that the highlight and select functions were adding about half of this time:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_113435" border="0" alt="2011-09-21_113435" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_113435_thumb.gif?resize=383%2C263" data-recalc-dims="1" />][12]

Maybe these can be optimized?

Instead of using dataTable.fnGetNodes(), I select the table id directly. Also, for the click event, I changed to use .live(‘click’, …) instead. This brought the time down to around ~50ms. That seems good enough for now.

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-09-21_121729" border="0" alt="2011-09-21_121729" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_121729_thumb.gif?resize=292%2C19" data-recalc-dims="1" />][13]

 [1]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/ie_slow_script_error.png
 [2]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_110622.gif
 [3]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_110654.gif
 [4]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_113120.gif
 [5]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_110734.gif
 [6]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_110748.gif
 [7]: http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112109.gif
 [8]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112217.gif
 [9]: http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112250.gif
 [10]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112422.gif
 [11]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_112532.gif
 [12]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_113435.gif
 [13]: http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/09/2011-09-21_121729.gif