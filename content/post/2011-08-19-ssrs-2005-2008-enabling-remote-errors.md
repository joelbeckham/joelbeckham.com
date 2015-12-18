---
title: 'SSRS 2005 / 2008: Enabling remote errors'
author: jbeckham
layout: post
date: 2011-08-19
url: /2011/08/ssrs-2005-2008-enabling-remote-errors/
categories:
  - DB
tags:
  - SSRS
---
<!-- [DocumentBodyStart:aafc7f4e-4161-4fe9-a058-763edad97dcf] -->

<pre class="csharpcode"><span class="kwrd">Use</span> ReportServer$SQL2008
<span class="kwrd">update</span> ConfigurationInfo <span class="kwrd">set</span> <span class="kwrd">Value</span> = <span class="str">'True'</span> <span class="kwrd">where</span>
Name = <span class="str">'EnableRemoteErrors'</span></pre>

<div class="jive-rendered-content">
</div>

<!-- [DocumentBodyEnd:aafc7f4e-4161-4fe9-a058-763edad97dcf] -->