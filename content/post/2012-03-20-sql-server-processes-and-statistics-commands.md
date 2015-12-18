---
title: 'SQL Server: Processes and Statistics commands'
author: jbeckham
layout: post
date: 2012-03-20
url: /2012/03/sql-server-processes-and-statistics-commands/
categories:
  - DB
---
I frequently forget these.

sp_who2 shows you the processes that are currently running. Using <a href="http://sqlserverplanet.com/dba/using-sp_who2/" target="_blank">sp_who2</a>.

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="2012-01-09_102118" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/2012-01-09_102118_thumb.gif?resize=672%2C115" alt="2012-01-09_102118" border="0" data-recalc-dims="1" />][1]

(Code for a better sp_who2 sproc: [http://sqlserverplanet.com/dmv-queries/a-better-sp\_who2-using-dmvs-sp\_who3/][2])

&nbsp;

Shows you the last statement sent from a client:

<div id="codeSnippetWrapper">
  <span class="lang:tsql decode:true crayon-inline">DBCC InputBuffer (<spid>)</span>
</div>

&nbsp;

Kill process:

<pre class="lang:tsql highlight:0 decode:true">KILL &lt;spid&gt;</pre>

Show IO statistics for query:

<span class="lang:tsql decode:true  crayon-inline ">SET STATISTICS TIME ON</span>

&nbsp;

Show how long parse, compilation, and execution of a query takes:

<pre class="lang:default decode:true ">SET STATISTICS IO ON</pre>

&nbsp;

<div id="codeSnippetWrapper">
  <p>
    &nbsp;
  </p>
</div>

 [1]: http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/2012-01-09_102118.gif
 [2]: http://sqlserverplanet.com/dmv-queries/a-better-sp_who2-using-dmvs-sp_who3/