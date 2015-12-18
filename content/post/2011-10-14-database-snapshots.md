---
title: Database Snapshots
author: jbeckham
layout: post
date: 2011-10-14
url: /2011/10/database-snapshots/
categories:
  - DB
---
<a href="http://msdn.microsoft.com/en-us/library/ms175876.aspx" target="_blank">CREATE Snapshot</a>:

<pre style="width: 577px; height: 128px">CREATE DATABASE AdventureWorks2008R2_dbss1800 ON
( NAME = AdventureWorks2008R2_Data, FILENAME = 
'C:Program FilesMicrosoft SQL ServerMSSQL10_50.MSSQLSERVERMSSQLDataAdventureWorks2008R2_data_1800.ss' )
AS SNAPSHOT OF AdventureWorks2008R2;
GO</pre>

Note that <font face="Courier New">NAME=AdventureWorks2008R2_Data</font> is the logical name of the source’s datafile

<a href="http://msdn.microsoft.com/en-us/library/ms189281.aspx" target="_blank">Revert to Snapshot</a>:

<pre style="width: 577px; height: 105px"><p>
  RESTORE DATABASE AdventureWorks2008R2 from 
  DATABASE_SNAPSHOT = 'AdventureWorks2008R2_dbss1800';
</p>

<p>
  GO
</p></pre>

Reverting will fail if other users are connected. Here’s how to put the database in single user mode:

    ALTER DATABASE YourDB<br />SET SINGLE_USER WITH<br />ROLLBACK IMMEDIATE

&#160;

(If you want to give open transactions time to finish, you can set <font face="Courier New">ROLLBACK AFTER 60</font>)

&#160;

Make sure to drop any other snapshots first

<a href="http://msdn.microsoft.com/en-us/library/ms190220.aspx" target="_blank">Drop Snapshot</a>:

<pre>DROP DATABASE SalesSnapshot0600</pre>