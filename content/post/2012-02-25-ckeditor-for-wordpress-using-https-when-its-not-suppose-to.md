---
title: CKEditor for WordPress using HTTPS when it's not suppose to
author: jbeckham
layout: post
date: 2012-02-25
url: /2012/02/ckeditor-for-wordpress-using-https-when-its-not-suppose-to/
categories:
  - Dev
tags:
  - Wordpress
---
I'm runnin WordPress on IIS. The latest version of CKEditor for WordPress seems to have an issue where I'm accessing the admin area with HTTP, but all the urls it generates (images, js files, etc) are being requested through HTTPS. I noticed it because I don't have HTTPS bound to my site at the moment and all of the CKEditor assets couldn't be found.

Digging in a bit, I found these lines in ckeditor_class.php:

<div id="codeSnippetWrapper">
  <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet"><span style="color: #0000ff">if</span>($_SERVER[<span style="color: #006080">'HTTPS'</span>]) {<br />    $siteurl = str_replace(<span style="color: #006080">'http:'</span>, <span style="color: #006080">'https:'</span>, $siteurl);<br />    $this-&gt;plugin_path = str_replace(<span style="color: #006080">'http:'</span>, <span style="color: #006080">'https:'</span>, $this-&gt;plugin_path);</pre>
  
  <p>
    </div> 
    
    <p>
      I found that $_SERVER['HTTPS'] was set to 'off', which would still cause the if statement to be true. Weird.
    </p>
    
    <p>
      I changed the if statement to:
    </p>
    
    <div id="codeSnippetWrapper">
      <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet"><span style="color: #0000ff">if</span>($_SERVER[<span style="color: #006080">'HTTPS'</span>] == <span style="color: #006080">'on'</span>) {</pre>
      
      <p>
        </div> 
        
        <p>
          This fixed the problem. I don't know enough about PHP to know if some environments set $_SERVER['HTTPS'] to true/false which would allow the original code to work, or if this is a bug in all environments.
        </p>