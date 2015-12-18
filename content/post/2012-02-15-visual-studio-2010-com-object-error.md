---
title: Visual Studio 2010 COM object error
author: jbeckham
layout: post
date: 2012-02-15
url: /2012/02/visual-studio-2010-com-object-error/
categories:
  - Dev
tags:
  - VisualStudio
---
I randomly started getting a, "COM object that has been separated from its underlying RCW cannot be used" error when trying to view a project&#8217;s properties in Visual Studio 2010:

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2012-02-15_125905" border="0" alt="2012-02-15_125905" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-15_125905_thumb.gif?resize=519%2C68" data-recalc-dims="1" />][1]

<a href="http://stackoverflow.com/questions/5926041/vs-2010-properties-page-fail-to-show-com-object-that-has-been-separated-from-its" target="_blank">This StackOverflow question</a> seems to indicate that it could be caused by one of my add-ins. The first step was to disable add-ins and see if the problem resolves. Go to Tools -> Options. Then Environment -> Add-in / Macros security and uncheck "Allow Add-in components to load."

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2012-02-15_130101" border="0" alt="2012-02-15_130101" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-15_130101_thumb.gif?resize=496%2C121" data-recalc-dims="1" />][2]

I restarted VS and the problem went away. The next step was to start eliminating the add-ins one-by-one to figure out the one causing the trouble. I removed one from the list of Add-in File Paths and restarted VS. Strangely, it didn&#8217;t save the change and the add-in directory was still there after the restart. That&#8217;s odd.

I finally was able to find where these settings are stored in the registry:

HKEY\_LOCAL\_MACHINESOFTWAREWow6432NodeMicrosoftVisualStudio10.0AutomationOptionsLookInFolders

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2012-02-15_131624" border="0" alt="2012-02-15_131624" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-15_131624_thumb.gif?resize=448%2C164" data-recalc-dims="1" />][3]

I delete the TestDriven.NET one first since that&#8217;s the one causing trouble in the StackOverflow post. I restarted VS and magically the error has gone away. Silly TestDriven.NET.

 [1]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-15_125905.gif
 [2]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-15_130101.gif
 [3]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-15_131624.gif