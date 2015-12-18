---
title: Misc SQL Statistics Queries
author: jbeckham
layout: post
date: 2012-02-10
url: /2012/02/misc-sql-statistics-queries/
categories:
  - DB
tags:
  - Performance
  - SQL
---
View statistics for a table:

<div id="codeSnippetWrapper">
  <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet"><span style="color: #0000ff">SELECT</span> name <span style="color: #0000ff">AS</span> stats_name, <br />    STATS_DATE(object_id, stats_id) <span style="color: #0000ff">AS</span> statistics_update_date,<br />    no_recompute<br /><span style="color: #0000ff">FROM</span> sys.stats <br /><span style="color: #0000ff">WHERE</span> object_id = OBJECT_ID(<span style="color: #006080">'dbo.csi_answer'</span>);</pre>
  
  <p>
    </div> 
    
    <p>
      Each statistics shows when it was last updated and if no_recompute is on:
    </p>
    
    <p>
      <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-09_111618.gif"><img style="background-image: none; border-right-width: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="2012-02-09_111618" border="0" alt="2012-02-09_111618" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-09_111618_thumb.gif?resize=416%2C42" data-recalc-dims="1" /></a>
    </p>
    
    <p>
      &#160;
    </p>
    
    <p>
      Database properties has a setting called "Auto Update Statistics":
    </p>
    
    <p>
      <a href="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-09_112136.gif"><img style="background-image: none; border-right-width: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="2012-02-09_112136" border="0" alt="2012-02-09_112136" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/02/2012-02-09_112136_thumb.gif?resize=516%2C221" data-recalc-dims="1" /></a>
    </p>
    
    <p>
      &#160;
    </p>
    
    <p>
      This sproc:
    </p>
    
    <div>
      <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet"><span style="color: #0000ff">EXEC</span> sp_updatestats</pre>
    </div>
    
    <div>
      &#160;
    </div>
    
    <div>
    </div>
    
    <p>
      runs UPDATE STATISTICS against all user-defined tables in the current database. The <a href="http://msdn.microsoft.com/en-us/library/ms173804.aspx" target="_blank">documentation for sp_updatestats</a> states this:
    </p>
    
    <blockquote>
      <p>
        <strong>sp_updatestats</strong> updates only the statistics that require updating based on the <strong>rowmodctr</strong> information in the <strong>sys.sysindexes</strong> catalog view, thus avoiding unnecessary updates of statistics on unchanged rows.
      </p>
    </blockquote>
    
    <p>
      RowModCTR can be found with this query:
    </p>
    
    <div id="codeSnippetWrapper">
      <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; background-color: #f4f4f4; margin: 0em; border-left-style: none; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; border-right-style: none; font-size: 8pt; overflow: visible; padding-top: 0px" id="codeSnippet"><span style="color: #0000ff">SELECT</span> * <span style="color: #0000ff">FROM</span> sys.sysindexes<br /><span style="color: #0000ff">WHERE</span> id = OBJECT_ID(<span style="color: #006080">'dbo.csi_answer'</span>)</pre>
      
      <p>
        </div>