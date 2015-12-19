---
title: Oracle character set settings
author: jbeckham
layout: post
date: 2012-04-02
url: /2012/04/oracle-character-set-settings/
categories:
  - DB
tags:
  - Oracle
---
Here are the [queries][1] to view the char and nchar character set settings:

select value from nls\_database\_parameters where parameter = 'NLS_CHARACTERSET';

select value from nls\_database\_parameters where parameter = 'NLS\_NCHAR\_CHARACTERSET';

These return AL32UTF8 for me, which apparently supersedes UTF8 (which is an older setting in Oracle for an older unicode specification which is missing some XML specific characters).

 [1]: http://www.adp-gmbh.ch/ora/database.html