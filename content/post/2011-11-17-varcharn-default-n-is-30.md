---
title: 'varchar[(n)] – Default n is 30'
author: jbeckham
layout: post
date: 2011-11-17
url: /2011/11/varcharn-default-n-is-30/
categories:
  - DB
---
I recently found a bug in a stored procedure which was truncating some string values. It turns out that they were being cast to varchar without n being specified. This resulted in them being cast to varchar(30) which was shorter than the input string.