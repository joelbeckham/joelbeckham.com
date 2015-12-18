---
title: URL Rewriting with WordPress on IIS 7
author: jbeckham
layout: post
date: 2011-08-16
url: /2011/08/url-rewriting-with-wordpress-on-iis-7/
categories:
  - Dev
tags:
  - IIS
  - Wordpress
---
  1. Make sure that the URL Rewrite module is installed. You can check / install through the WebPI installer. 
  2. Add the following configuration into the system.Webserver section of the web.config at the root of the wordpress site: <pre style="width: 547px; height: 292px" class="csharpcode"><span class="kwrd">&lt;</span><span class="html">rewrite</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;</span><span class="html">rules</span><span class="kwrd">&gt;</span>
        <span class="kwrd">&lt;</span><span class="html">rule</span> <span class="attr">name</span><span class="kwrd">="Main Rule"</span> <span class="attr">stopProcessing</span><span class="kwrd">="true"</span><span class="kwrd">&gt;</span>
            <span class="kwrd">&lt;</span><span class="html">match</span> <span class="attr">url</span><span class="kwrd">=".*"</span> <span class="kwrd">/&gt;</span>
            <span class="kwrd">&lt;</span><span class="html">conditions</span> <span class="attr">logicalGrouping</span><span class="kwrd">="MatchAll"</span><span class="kwrd">&gt;</span>
                <span class="kwrd">&lt;</span><span class="html">add</span> <span class="attr">input</span><span class="kwrd">="{REQUEST_FILENAME}"</span> <span class="attr">matchType</span><span class="kwrd">="IsFile"</span> <span class="attr">negate</span><span class="kwrd">="true"</span> <span class="kwrd">/&gt;</span>
                <span class="kwrd">&lt;</span><span class="html">add</span> <span class="attr">input</span><span class="kwrd">="{REQUEST_FILENAME}"</span> <span class="attr">matchType</span><span class="kwrd">="IsDirectory"</span> <span class="attr">negate</span><span class="kwrd">="true"</span> <span class="kwrd">/&gt;</span>
            <span class="kwrd">&lt;/</span><span class="html">conditions</span><span class="kwrd">&gt;</span>
            <span class="kwrd">&lt;</span><span class="html">action</span> <span class="attr">type</span><span class="kwrd">="Rewrite"</span> <span class="attr">url</span><span class="kwrd">="index.php"</span> <span class="kwrd">/&gt;</span>
        <span class="kwrd">&lt;/</span><span class="html">rule</span><span class="kwrd">&gt;</span>
    <span class="kwrd">&lt;/</span><span class="html">rules</span><span class="kwrd">&gt;</span>
<span class="kwrd">&lt;/</span><span class="html">rewrite</span><span class="kwrd">&gt;</span></pre>

More detailed instructions: <http://learn.iis.net/page.aspx/466/enabling-pretty-permalinks-in-wordpress/>