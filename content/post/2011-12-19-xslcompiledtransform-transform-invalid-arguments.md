---
title: XslCompiledTransform.Transform Invalid Arguments
author: jbeckham
layout: post
date: 2011-12-19
url: /2011/12/xslcompiledtransform-transform-invalid-arguments/
categories:
  - Dev
---
I kept getting this mysterious error on only one of the TeamCity build agents. The application compiles fine everywhere else.

_<font color="#a5a5a5">error CS1502: The best overloaded method match for &#8216;System.Xml.Xsl.XslCompiledTransform.Transform(System.Xml.XmlReader, System.Xml.Xsl.XsltArgumentList, System.Xml.XmlWriter, System.Xml.XmlResolver)' has some invalid arguments</font>_

The last line throws the error:

<div id="codeSnippetWrapper">
  <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet">
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">&#160;</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">var xslt = <span style="color: #0000ff">new</span> XslCompiledTransform();</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">...</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">XPathNavigator nav = xd.CreateNavigator();</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: white; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">...</pre>
    
    <p>
      <!--CRLF-->
    </p>
    
    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px">xslt.Transform(nav, xslArgs, xmlWriter, <span style="color: #0000ff">null</span>); <span style="color: #008000">// this line throws the error</span></pre>
    
    <p>
      <!--CRLF--></div> </div> 
      
      <p>
        That's really strange because Visual Studio says that I'm calling a valid overload. It compiles on my machine and on our other build agent.I thought this was a clue, but installing the SDK didn't make any difference:
      </p>
      
      <p>
        <font color="#a5a5a5"><em>Could not locate the expected version of the Microsoft Windows SDK. Looked for a location specified in the "InstallationFolder" value of the registry key "HKEY_LOCAL_MACHINESOFTWAREMicrosoftMicrosoft SDKsWindowsv6.0A". If your build process does not need the SDK then this can be ignored. Otherwise you can solve the problem by doing one of the following: 1) Install the Microsoft Windows SDK for Windows Server 2008 and .NET Framework 3.5. 2) Install Visual Studio 2008. 3) Manually set the above registry key to the correct location.</em></font>
      </p>
      
      <p>
        I also tried and failed with this solution: <a href="http://support.microsoft.com/kb/2431806">http://support.microsoft.com/kb/2431806</a>
      </p>
      
      <p>
        I finally found this <a href="http://support.microsoft.com/kb/968556" target="_blank">MS KB article</a> which describes the problem exactly. The problem is that it refers you to a hotfix that you have to obtain from MS Support. I was able to find it here: <a href="http://thehotfixshare.net/board/index.php?showtopic=15089">http://thehotfixshare.net/board/index.php?showtopic=15089</a>. Installing the hotfix resolved the issue.
      </p>