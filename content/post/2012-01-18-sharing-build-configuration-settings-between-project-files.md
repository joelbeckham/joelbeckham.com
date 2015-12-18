---
title: Sharing Build Configuration Settings Between Project Files
author: jbeckham
layout: post
date: 2012-01-18
url: /2012/01/sharing-build-configuration-settings-between-project-files/
categories:
  - Dev
tags:
  - Build
---
_**Update:** Oh snap&#8230; [nCrunch][1] isn&#8217;t smart enough to pull in the external configurations like this, and so it won&#8217;t run any of my tests. Gotta  find plan B._

&nbsp;

As we&#8217;ve added new projects to our solution and new build environments, it has become increasingly difficult to maintain consistency in our settings across all projects. Here is how we addressed it.

  1. Added a new MSBuild target file (CommonBuildConfigurationSettings.target) to the solution to contain these settings.[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="2012-01-17_164355" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/01/2012-01-17_164355_thumb.gif?resize=244%2C139" alt="2012-01-17_164355" border="0" data-recalc-dims="1" />][2]
  2. Added the shared settings to CommonBuildConfigurationSettings.target. Note that we&#8217;ve added build settings for each of the project build configurations we have. To add a new project build configuration, a new section can simply be added here:[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="2012-01-17_165134" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/01/2012-01-17_165134_thumb.gif?resize=601%2C510" alt="2012-01-17_165134" border="0" data-recalc-dims="1" />][3]
  3. Removed these settings from the individual projects and replaced them with an import of the target file. <div id="codeSnippetWrapper">
      <div id="codeSnippet" style="text-align: left; line-height: 12pt; background-color: #f4f4f4; width: 100%; font-family: 'Courier New', courier, monospace; direction: ltr; color: black; font-size: 8pt; overflow: visible; border-style: none; padding: 0px;">
        <pre style="text-align: left; line-height: 12pt; background-color: white; margin: 0em; width: 100%; font-family: 'Courier New', courier, monospace; direction: ltr; color: black; font-size: 8pt; overflow: visible; border-style: none; padding: 0px;"><span id="lnum1" style="color: #606060;"> 1:</span> <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Import</span> <span style="color: #ff0000;">Project</span><span style="color: #0000ff;">="../Build/CommonBuildConfigurationSettings.target"</span><span style="color: #0000ff;">/&gt;</span></pre>
        
        <p>
          &nbsp;
        </p>
      </div>
    </div>

The benefits:

  * A single point to modify and add build configuration settings.
  * These settings can still be viewed by going to the Build tab of the Project Properties.
  * The solution configuration manager can still see all of the build configurations so you can still wire up the project configurations with the solution configurations as before.
  * The common shared settings can be overridden for a specific project if needed by modifying the values visible on the Build tab of the Project Properties.

The downsides:

  * Updating shared settings must be done through the target file and not the Build tab of the Project Properties. If someone forgets this and modifies through the Build tab, they will unintentially create an override for that one project.
  * Target files are cached in Visual Studio, so any changes to the shared configuration target file are not realized in Visual Studio until the solution is closed and reloaded.
  * Newly added projects have to be modified with the steps above.

 [1]: http://www.ncrunch.net/
 [2]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/01/2012-01-17_164355.gif
 [3]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/01/2012-01-17_165134.gif