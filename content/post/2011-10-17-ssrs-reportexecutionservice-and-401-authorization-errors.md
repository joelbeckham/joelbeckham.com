---
title: SSRS ReportExecutionService and 401 Authorization Errors
author: jbeckham
layout: post
date: 2011-10-17
url: /2011/10/ssrs-reportexecutionservice-and-401-authorization-errors/
categories:
  - DB
tags:
  - SSRS
---
&#160;

I was calling the SSRS Web service from the same machine and suddenly started getting 401 Authorization Errors. I finally found the cause.

Previously, I had been accessing the webservice with “localhost” in the URL, but at some point it got changed to the machine name. That’s when it stopped working. Apparently, a windows security feature called the “Lookback Check” causes this.