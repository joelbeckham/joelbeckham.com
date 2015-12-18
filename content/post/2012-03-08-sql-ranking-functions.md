---
title: SQL Ranking Functions
author: jbeckham
layout: post
date: 2012-03-08
url: /2012/03/sql-ranking-functions/
categories:
  - DB
tags:
  - SQL
---
&#160;

**<a href="http://msdn.microsoft.com/en-us/library/ms176102.aspx" target="_blank">Rank</a>:** Returns the rank of each row within the partition of a result set. The rank of a row is one plus the number of ranks that come before the row in question.

If two or more rows tie for a rank, each **tied rows receives the same rank**. For example, if the two top salespeople have the same SalesYTD value, they are both ranked one. The salesperson with the next highest SalesYTD is ranked number three, because there are two rows that are ranked higher. Therefore, the RANK function **does not always return consecutive integers**.

**<a href="http://msdn.microsoft.com/en-us/library/ms173825.aspx" target="_blank">Dense_Rank</a>:** Returns the rank of rows within the partition of a result set, without any gaps in the ranking. The rank of a row is one plus the number of distinct ranks that come before the row in question.

If two or more rows tie for a rank in the same partition, each tied **rows receives the same rank**. For example, if the two top salespeople have the same SalesYTD value, they are both ranked one. The salesperson with the next highest SalesYTD is ranked number two. This is one more than the number of distinct rows that come before this row. Therefore, the numbers returned by the DENSE_RANK function **do not have gaps** and always have consecutive ranks.

**<a href="http://msdn.microsoft.com/en-us/library/ms186734.aspx" target="_blank">Row_Number</a>:** Returns the sequential number of a row within a partition of a result set, starting at 1 for the first row in each partition. **There are no repeated values or gaps**.

**<a href="http://msdn.microsoft.com/en-us/library/ms175126.aspx" target="_blank">NTile</a>:** Distributes the rows in an ordered partition into a specified number of groups. The groups are numbered, starting at one. For each row, NTILE returns the number of the group to which the row belongs.