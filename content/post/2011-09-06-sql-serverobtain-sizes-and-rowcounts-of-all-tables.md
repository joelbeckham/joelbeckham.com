---
title: SQL Server–Obtain sizes and rowcounts of all tables
author: jbeckham
layout: post
date: 2011-09-06
url: /2011/09/sql-serverobtain-sizes-and-rowcounts-of-all-tables/
categories:
  - DB
---
<http://therightstuff.de/CommentView,guid,df930155-f60f-4f56-ab33-f1352ff091a1.aspx> 

&#160;

<pre style="width: 577px; height: 380px" class="csharpcode"><span class="kwrd">CREATE</span> <span class="kwrd">TABLE</span> #t 
( 
    [name] NVARCHAR(128),
    [<span class="kwrd">rows</span>] <span class="kwrd">CHAR</span>(11),
    reserved <span class="kwrd">VARCHAR</span>(18), 
    <span class="kwrd">data</span> <span class="kwrd">VARCHAR</span>(18), 
    index_size <span class="kwrd">VARCHAR</span>(18),
    unused <span class="kwrd">VARCHAR</span>(18)
) 

INSERT #t <span class="kwrd">EXEC</span> sp_msForEachTable <span class="str">'EXEC sp_spaceused '</span><span class="str">'?'</span><span class="str">''</span> 

<span class="kwrd">SELECT</span> *
<span class="kwrd">FROM</span>   #t

<span class="kwrd">DROP</span> <span class="kwrd">TABLE</span> #t </pre>