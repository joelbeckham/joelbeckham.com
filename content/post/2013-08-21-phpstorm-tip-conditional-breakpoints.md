---
title: 'PHPStorm Tip &#8211; Conditional Breakpoints'
author: jbeckham
layout: post
date: 2013-08-21
url: /2013/08/phpstorm-tip-conditional-breakpoints/
cudazi_post_settings:
  - default
categories:
  - Dev
  - PHP
---
### Simple Condition:

<div>
  <p>
    After creating a breakpoint -> right click -> Edit. The conditions box lets you enter the conditions under which the breakpoint will suspend execution.
  </p>
  
  <p>
    <a href="http://www.joelbeckham.com/blog/2013/08/21/phpstorm-tip-conditional-breakpoints/breakpoint-conditional/" rel="attachment wp-att-464"><img class="alignnone size-full wp-image-464" alt="breakpoint-conditional" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2013/08/breakpoint-conditional1.png?fit=499%2C197" data-recalc-dims="1" /></a>
  </p>
</div>

### Break only if another breakpoint has been hit:

<div>
  I&#8217;ve found this really handy for functions that get called a lot, but I only want it to suspend when it&#8217;s been called from a specific place. This is great, for example, if I want to only break on a line after it&#8217;s been called by a specific test. Here&#8217;s how:
</div>

<div>
</div>

<div>
  1. Set a breakpoint in the unit test. Right click -> Edit -> Uncheck &#8216;Suspend&#8217; (because I don&#8217;t actually want it to stop here)
</div>

<div>
  <img class="alignnone size-full wp-image-466" alt="breakpoint-trigger" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2013/08/breakpoint-trigger1.png?fit=553%2C271" data-recalc-dims="1" />
</div>

<div>
</div>

<div>
</div>

<div>
  2. Set a breakpoint on the line I actually want to suspend on. Right click -> Edit -> Uncheck &#8216;Suspend&#8217;, Select the breakpoint from step #1 in the &#8220;Disabled until selected breakpoint is hit&#8221;. If you have so many breakpoints that its hard to find the one you want, see the last tip below.
</div>

<div>
</div>

<div>
  <img class="alignnone size-full wp-image-465" alt="breakpoint-target" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2013/08/breakpoint-target1.png?fit=528%2C366" data-recalc-dims="1" />
</div>

### Bulk edit / delete breakpoints:

<div>
  You can get to the bulk edit screen using any of these methods:
</div>

<div>
  <ul>
    <li>
      Ctrl + Shift + F8
    </li>
    <li>
      Right Click on a Breakpoint and click &#8220;View Breakpoints&#8221;
    </li>
    <li>
      Menu: Run ->View Breakpoints
    </li>
  </ul>
  
  <div>
    Within the dialog, hitting Ctrl + A then Delete will remove all breakpoints.
  </div>
</div>