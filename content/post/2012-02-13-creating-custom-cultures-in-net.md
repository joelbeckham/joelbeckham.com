---
title: Creating Custom Cultures in .NET
author: jbeckham
layout: post
date: 2012-02-13
url: /2012/02/creating-custom-cultures-in-net/
categories:
  - Dev
tags:
  - Globalization
---
Our application receives a culture name (e.g. en-US, de-DE, ja-JP) as user input and in response returns customized content. The problem is that there is a specific use case for Japanese (ja-JP) in which the content needs to be different than the other Japanese use cases. We want to leave all the other use cases alone.

We have chosen to solve this is by creating a new culture to represent the this special case &#8211; <a href="http://msdn.microsoft.com/en-us/library/system.globalization.cultureandregioninfobuilder.cultureandregioninfobuilder.aspx" target="_blank">CultureAndRegionInfoBuilder</a> does exactly that.

Here is a crude proof of concept:

<div id="codeSnippetWrapper">
  <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> var customCultures = CultureInfo.GetCultures(CultureTypes.UserCustomCulture);</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum2">   2:</span> <span style="color: #0000ff">if</span> (!customCultures.Any(c =&gt; c.Name == <span style="color: #006080">"X-ja-JP-Test"</span>))</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum3">   3:</span> {</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum4">   4:</span>     var newCulture = <span style="color: #0000ff">new</span> CultureAndRegionInfoBuilder(<span style="color: #006080">"X-ja-JP-Test"</span>, CultureAndRegionModifiers.None);</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum5">   5:</span>     var existingCultureInfo = <span style="color: #0000ff">new</span> CultureInfo(<span style="color: #006080">"ja-JP"</span>);</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum6">   6:</span>     var existingRegionInfo = <span style="color: #0000ff">new</span> RegionInfo(<span style="color: #006080">"JP"</span>);</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum7">   7:</span>     newCulture.LoadDataFromCultureInfo(existingCultureInfo);</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum8">   8:</span>     newCulture.LoadDataFromRegionInfo(existingRegionInfo);</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum9">   9:</span>&#160; </pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum10">  10:</span>     newCulture.Register();</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum11">  11:</span> }</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum12">  12:</span>&#160; </pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum13">  13:</span> var customJapanese = <span style="color: #0000ff">new</span> CultureInfo(<span style="color: #006080">"X-ja-JP-Test"</span>);</pre>
    
    <p>
      <!--CRLF--></div> </div> 
      
      <p>
        &#160;
      </p>
      
      <p>
        Breaking this down, I first check to see if the custom culture has already been added. When the culture is registered, it is persisted and does not need to be recreated each time it is needed.
      </p>
      
      <p>
        Then a call to the CultureAndRegionInfoBuilder constructor:
      </p>
      
      <div id="codeSnippetWrapper">
        <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #0000ff">public</span> CultureAndRegionInfoBuilder(</pre>
          
          <p>
            <!--CRLF-->
          </p>
          
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">    <span style="color: #0000ff">string</span> cultureName,</pre>
          
          <p>
            <!--CRLF-->
          </p>
          
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">    CultureAndRegionModifiers flags</pre>
          
          <p>
            <!--CRLF-->
          </p>
          
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">)</pre>
          
          <p>
            <!--CRLF--></div> </div> 
            
            <p>
              &#160;
            </p>
            
            <p>
              Here&#8217;s what the documentation says about naming (cultureName) a new custom culture:
            </p>
            
            <blockquote>
              <p>
                The preferred format of the cultureName parameter for a new, custom culture is "[prefix-]language[-region][-suffix[…]]", where the language component is required and the prefix, region, and suffix components are optional. The maximum length of each component is 8 characters and the maximum length of the entire cultureName parameter is 84 characters.
              </p>
              
              <p>
                The prefix component is the Internet Assigned Numbers Authority (IANA) identification. Specify "i-" or "I-" for culture names registered with the IANA, or "x-" or "X-" for culture names reserved for private use. Otherwise, the prefix is not required. For more information, see RFC 4646, "Tags for the Identification of Languages."
              </p>
              
              <p>
                The language component of the cultureName parameter specifies a lowercase two-letter code derived from ISO 639-1, and region specifies an uppercase two-letter code derived from ISO 3166. For example, "en-US" stands for English as spoken in the United States. The absence of the region component signifies a neutral culture.
              </p>
            </blockquote>
            
            <p>
              The second parameter specifies if it replaces an existing culture, is a neutral culture, or is a new one (CultureAndRegionModifiers.None). After that, I populate the new culture from the existing Japanese Culture and Region information.
            </p>
            
            <p>
              Then the new culture needs to be registered:
            </p>
            
            <div id="codeSnippetWrapper">
              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">newCulture.Register();</pre>
            </div>
            
            <p>
              &#160;
            </p>
            
            <p>
              Admin privileges are required because it creates a .nlp file in %windir%Globalization to persist it.
            </p>
            
            <p>
              <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-13_120838.gif"><img style="background-image: none; border-right-width: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="2012-02-13_120838" border="0" alt="2012-02-13_120838" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-13_120838_thumb.gif?resize=176%2C179" data-recalc-dims="1" /></a>
            </p>
            
            <p>
              &#160;
            </p>
            
            <p>
              Once registered, the new culture can be instantiated with CultureInfo just like pre-defined cultures:
            </p>
            
            <div id="codeSnippetWrapper">
              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">var customJapanese = <span style="color: #0000ff">new</span> CultureInfo(<span style="color: #006080">"X-ja-JP-Test"</span>);</pre>
              
              <p>
                </div> 
                
                <p>
                  &#160;
                </p>
                
                <p>
                  MSDN How To: <a href="http://msdn.microsoft.com/en-us/library/ms172469.aspx" target="_blank">How to Create Custom Cultures</a>
                </p>