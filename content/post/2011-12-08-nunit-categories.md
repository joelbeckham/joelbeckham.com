---
title: NUnit Categories
author: jbeckham
layout: post
date: 2011-12-08
url: /2011/12/nunit-categories/
categories:
  - Dev
tags:
  - Testing
---
Sometimes I want to only run a portion of my tests. nUnit allows tests to be labeled with Categories and then selectively choose which categories you want to run. I have found this especially helpful on TeamCity for integration tests because I don't have all the infrastructure set up to successfully execute all of my tests. I have created a Category called "Always" and marked the tests that can run on TeamCity with this category.

Here's how to categorize tests. There is a Category Attribute that can be added on the Test level:

<div id="codeSnippetWrapper">
  <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">[Test]</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">[Category(<span style="color: #006080">"Always"</span>)]</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #0000ff">public</span> <span style="color: #0000ff">void</span> TheTest()</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">{</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">}</pre>
    
    <p>
      <!--CRLF--></div> </div> 
      
      <p>
        on the Class level:
      </p>
      
      <div id="codeSnippetWrapper">
        <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">[TestFixture]</pre>
          
          <p>
            <!--CRLF-->
          </p>
          
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">[Category(<span style="color: #006080">"Always"</span>)]</pre>
          
          <p>
            <!--CRLF-->
          </p>
          
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> TheTestFixture</pre>
          
          <p>
            <!--CRLF-->
          </p>
          
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">{</pre>
          
          <p>
            <!--CRLF--></div> </div> 
            
            <p>
              or at the assembly level (in AssemblyInfo.cs)
            </p>
            
            <div id="codeSnippetWrapper">
              <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
                <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">[assembly: NUnit.Framework.Category(<span style="color: #006080">"Always"</span>)]</pre>
                
                <p>
                  <!--CRLF--></div> </div> 
                  
                  <p>
                  </p>
                  
                  <p>
                    Once marked, then nUnit allows you filter which categories you want to run. Select the "Categories" tab and then choose the categories you wish to run unit tests on:
                  </p>
                  
                  <p>
                    <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/12/2011-12-13_132205.gif"><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-12-13_132205" border="0" alt="2011-12-13_132205" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/12/2011-12-13_132205_thumb.gif?resize=351%2C330" data-recalc-dims="1" /></a>
                  </p>
                  
                  <p>
                    Now all tests that aren't in the selected category are grayed out and do not run:
                  </p>
                  
                  <p>
                    <a href="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/12/2011-12-13_132320.gif"><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-12-13_132320" border="0" alt="2011-12-13_132320" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/12/2011-12-13_132320_thumb.gif?resize=336%2C78" data-recalc-dims="1" /></a>
                  </p>
                  
                  <p>
                    In TeamCity, this can be configured under the NUnit Build Step configuration:
                  </p>
                  
                  <p>
                    <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/12/2011-12-13_132415.gif"><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="2011-12-13_132415" border="0" alt="2011-12-13_132415" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/12/2011-12-13_132415_thumb.gif?resize=505%2C215" data-recalc-dims="1" /></a>
                  </p>