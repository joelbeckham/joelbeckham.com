---
title: GUID vs Int
author: jbeckham
layout: post
date: 2012-01-27
url: /2012/01/guid-vs-int/
categories:
  - DB
---
Here’s an interesting insight to follow up on a discussion I had the other day about using GUIDs vs Ints as primary keys.

The database I work on uses Int’s for its primary keys. The largest table has accumulated 14 million rows since inception (2005). At its current size, if we switched the primary keys to Guids, it would add about 1.2 GB to the database (taking into consideration the indexes as well as foreign key references). One concern brought up about using Int’s is hitting the maximum value. If we accelerated this one table’s growth to 14 million rows per year (instead of since its inception), here’s when we would hit the cap for various data types:

· Int (4 bytes): 153 years

· BigInt (8 bytes): 658,812,288,000 years

· Guid (16 bytes): 2.42857143 × 10^31 years