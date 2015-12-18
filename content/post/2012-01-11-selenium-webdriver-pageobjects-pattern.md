---
title: 'Selenium WebDriver: PageObjects Pattern'
author: jbeckham
layout: post
date: 2012-01-11
url: /2012/01/selenium-webdriver-pageobjects-pattern/
categories:
  - Dev
tags:
  - Selenium
  - Testing
---
As you increase the number of functional tests against your site, you will find a lot of duplicate code. This increasingly makes maintenance difficult because a single UI change will require many changes across the tests. In response, Selenium has suggested the <a href="http://code.google.com/p/selenium/wiki/PageObjects" target="_blank">PageObjects</a> pattern which represents each page on your site as an object. The details of interacting with a page is moved out of the test and into the page object. The page object exposes the "services" that the page offers, and your tests then interact with these "services". When you need to make a UI change, you only have to make a single change to the related page object.

The key here is that there should <u>_only be one_</u> place that knows about the HTML structure of a given page.

Here is a simple example of the PageObject pattern: 

<div id="codeSnippetWrapper">
  <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> SurveyPage</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum2">   2:</span> {</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum3">   3:</span>     <span style="color: #0000ff">private</span> IWebDriver driver;</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum4">   4:</span>  </pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum5">   5:</span>     <span style="color: #0000ff">public</span> SurveyPage(IWebDriver driver)</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum6">   6:</span>     {</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum7">   7:</span>         <span style="color: #0000ff">this</span>.driver = driver;</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum8">   8:</span>  </pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum9">   9:</span>         <span style="color: #008000">// Check that we're on the right page</span></pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum10">  10:</span>         <span style="color: #0000ff">if</span> (driver.Title != <span style="color: #006080">"CSI Survey"</span>)</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum11">  11:</span>         {</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum12">  12:</span>             <span style="color: #0000ff">throw</span> <span style="color: #0000ff">new</span> InvalidElementStateException(<span style="color: #006080">"Page Title is ""</span> + driver.Title + <span style="color: #006080">"" but expected to be "CSI Survey""</span>);</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum13">  13:</span>         }</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum14">  14:</span>     }</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum15">  15:</span>  </pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum16">  16:</span>     <span style="color: #008000">// Conceptually, the Survey Page offers the user the "service" to see what language is currently selected.</span></pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum17">  17:</span>     <span style="color: #0000ff">public</span> <span style="color: #0000ff">string</span> GetSelectedLanguage()</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum18">  18:</span>     {</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum19">  19:</span>         var selectedLanguage = driver.FindElement(By.Id(<span style="color: #006080">"SurveyUC_LanguageDD"</span>))</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum20">  20:</span>             .FindElement(By.CssSelector(<span style="color: #006080">"option[selected="selected"]"</span>)).Text;</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum21">  21:</span>         <span style="color: #0000ff">return</span> selectedLanguage;</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum22">  22:</span>     }</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum23">  23:</span> }</pre>
    
    <p>
      <!--CRLF--></div> </div> 
      
      <p>
        &#160;
      </p>
      
      <p>
        Note that the constructor validates that we&#8217;re on the right page. Now if you want to check that the expected language is selected, you can write this in your test:
      </p>
      
      <div id="codeSnippetWrapper">
        <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> var page = <span style="color: #0000ff">new</span> SurveyPage(driver);</pre>
          
          <p>
            <!--CRLF-->
          </p>
          
          <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum2">   2:</span> Assert.That(page.GetSelectedLanguage(), Is.EqualTo(<span style="color: #006080">"English ("US")"</span>));</pre>
          
          <p>
            <!--CRLF--></div> </div> 
            
            <p>
              &#160;
            </p>
            
            <p>
              If at some point, you change the controls for showing the language selection, you only have to update the SurveyPage class and none of the tests will know any different.
            </p>
            
            <p>
              &#160;
            </p>
            
            <h3>
              PageFactory
            </h3>
            
            <p>
              While using this pattern significantly improves the readability and maintainability of your code, there is still a lot of boiler-plate code that gets repeated. Selenium provides the <a href="http://code.google.com/p/selenium/wiki/PageFactory" target="_blank">PageFactory</a> to address this issue. From the test, this PageFactory is used like this (note that line 2 is the only difference between this and the last example):
            </p>
            
            <div id="codeSnippetWrapper">
              <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
                <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> var page = <span style="color: #0000ff">new</span> SurveyPage(driver);</pre>
                
                <p>
                  <!--CRLF-->
                </p>
                
                <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum2">   2:</span> PageFactory.InitElements(driver, page);</pre>
                
                <p>
                  <!--CRLF-->
                </p>
                
                <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum3">   3:</span> Assert.That(page.GetSelectedLanguage(), Is.EqualTo(<span style="color: #006080">"English ("US")"</span>));</pre>
                
                <p>
                  <!--CRLF--></div> </div> 
                  
                  <p>
                    &#160;
                  </p>
                  
                  <p>
                    The SurveyPage class can be changed as follows. First, a public property is created to represent the Language Drop-down control:
                  </p>
                  
                  <div id="codeSnippetWrapper">
                    <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
                      <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff">public</span> IWebElement LanguageDropdown { get; set; }</pre>
                      
                      <p>
                        <!--CRLF--></div> </div> 
                        
                        <p>
                          &#160;
                        </p>
                        
                        <p>
                          By default, the PageFactory will populate this with a control with an ID that matches the property name, LanguageDropdown in this case. Sine our control has a different name, we can make use of the FindsBy Attribute to specify how the control is found:
                        </p>
                        
                        <div id="codeSnippetWrapper">
                          <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
                            <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> [FindsBy(How = How.Id, Using = <span style="color: #006080">"SurveyUC_LanguageDD"</span>)]</pre>
                            
                            <p>
                              <!--CRLF-->
                            </p>
                            
                            <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum2">   2:</span> <span style="color: #0000ff">public</span> IWebElement LanguageDropdown { get; set; }</pre>
                            
                            <p>
                              <!--CRLF--></div> </div> 
                              
                              <p>
                                &#160;
                              </p>
                              
                              <p>
                                This this property in place, we can modify GetSelectedLanguage():
                              </p>
                              
                              <div id="codeSnippetWrapper">
                                <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
                                  <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">string</span> GetSelectedLanguage()</pre>
                                  
                                  <p>
                                    <!--CRLF-->
                                  </p>
                                  
                                  <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum2">   2:</span> {</pre>
                                  
                                  <p>
                                    <!--CRLF-->
                                  </p>
                                  
                                  <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum3">   3:</span>     var selectedLanguage = LanguageDropdown.FindElement(By.CssSelector(<span style="color: #006080">"option[selected="selected"]"</span>)).Text;</pre>
                                  
                                  <p>
                                    <!--CRLF-->
                                  </p>
                                  
                                  <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum4">   4:</span>     <span style="color: #0000ff">return</span> selectedLanguage;</pre>
                                  
                                  <p>
                                    <!--CRLF-->
                                  </p>
                                  
                                  <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum5">   5:</span> }</pre>
                                  
                                  <p>
                                    <!--CRLF--></div> </div> 
                                    
                                    <p>
                                      &#160;
                                    </p>
                                    
                                    <p>
                                      This really starts to pay off as the number of elements on the page that you want to interact with increases as well as when you are interacting with the same elements in multiple methods. One last improvement to be made is moving the page title check, and the PageFactory initialization into a base class:
                                    </p>
                                    
                                    <div id="codeSnippetWrapper">
                                      <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> WebDriverBasePage</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum2">   2:</span> {</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum3">   3:</span>     <span style="color: #0000ff">protected</span> IWebDriver driver;</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum4">   4:</span>  </pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum5">   5:</span>     <span style="color: #0000ff">public</span> WebDriverBasePage(IWebDriver driver, <span style="color: #0000ff">string</span> expectedTitle)</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum6">   6:</span>     {</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum7">   7:</span>         <span style="color: #0000ff">this</span>.driver = driver;</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum8">   8:</span>  </pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum9">   9:</span>         <span style="color: #008000">// Check that we're on the right page</span></pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum10">  10:</span>         <span style="color: #0000ff">if</span> (driver.Title != expectedTitle)</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum11">  11:</span>         {</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum12">  12:</span>             <span style="color: #0000ff">throw</span> <span style="color: #0000ff">new</span> InvalidElementStateException(<span style="color: #006080">"Page Title is ""</span> + driver.Title + <span style="color: #006080">"" but expected to be ""</span> + expectedTitle + <span style="color: #006080">"""</span>);</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum13">  13:</span>         }</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum14">  14:</span>  </pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum15">  15:</span>         PageFactory.InitElements(driver, <span style="color: #0000ff">this</span>);</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum16">  16:</span>     }</pre>
                                        
                                        <p>
                                          <!--CRLF-->
                                        </p>
                                        
                                        <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum17">  17:</span> }</pre>
                                        
                                        <p>
                                          <!--CRLF--></div> </div> 
                                          
                                          <p>
                                            &#160;
                                          </p>
                                          
                                          <p>
                                            Now the SurveyPage can be reduced down to this:
                                          </p>
                                          
                                          <div id="codeSnippetWrapper">
                                            <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> SurveyPage : WebDriverBasePage</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum2">   2:</span> {</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum3">   3:</span>     [FindsBy(How = How.Id, Using = <span style="color: #006080">"SurveyUC_LanguageDD"</span>)]</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum4">   4:</span>     <span style="color: #0000ff">public</span> IWebElement LanguageDropdown { get; set; }</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum5">   5:</span>  </pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum6">   6:</span>     <span style="color: #0000ff">public</span> SurveyPage(IWebDriver driver)</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum7">   7:</span>         : <span style="color: #0000ff">base</span> (driver, <span style="color: #006080">"CSI Survey"</span>)</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum8">   8:</span>     {</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum9">   9:</span>     }</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum10">  10:</span>  </pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum11">  11:</span>     <span style="color: #0000ff">public</span> <span style="color: #0000ff">string</span> GetSelectedLanguage()</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum12">  12:</span>     {</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum13">  13:</span>         var selectedLanguage = LanguageDropdown.FindElement(By.CssSelector(<span style="color: #006080">"option[selected="selected"]"</span>)).Text;</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum14">  14:</span>         <span style="color: #0000ff">return</span> selectedLanguage;</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum15">  15:</span>     }</pre>
                                              
                                              <p>
                                                <!--CRLF-->
                                              </p>
                                              
                                              <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum16">  16:</span> }</pre>
                                              
                                              <p>
                                                <!--CRLF--></div> </div> 
                                                
                                                <p>
                                                  &#160;
                                                </p>
                                                
                                                <p>
                                                  Things to keep in mind:
                                                </p>
                                                
                                                <ul>
                                                  <li>
                                                    PageObjects should not expose the underlying WebDriver instance.
                                                  </li>
                                                  <li>
                                                    When linking from one page to the next, return a page class.
                                                  </li>
                                                  <li>
                                                    Elements using the FindsBy attribute are looked up each time the property is accessed. If it&#8217;s an element that doesn&#8217;t change, this can be optimized by applying the [CacheLookup] attribute to the property.
                                                  </li>
                                                </ul>