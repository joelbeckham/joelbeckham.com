---
title: Custom Assemblies in SSRS 2008
author: jbeckham
layout: post
date: 2011-10-14
url: /2011/10/custom-assemblies-in-ssrs-2008/
categories:
  - DB
tags:
  - SSRS
---
Visual Studio can compile a report just fine, but then report that the report definition is invalid when you try to deploy.

In addition to putting the custom assembly SSRS’s bin folder: _<font color="#a5a5a5" size="2" face="Courier New">C:Program FilesMicrosoft SQL ServerMSRS10_50.MSSQLSERVERReporting ServicesReportServerbin</font>_

You have to put the assembly in VS’s private assemblies folder: <font color="#a5a5a5" face="Courier New"><em>C:Program Files (x86)Microsoft Visual Studio 2008Common7IDEPrivateAssemblies</em></font>

Otherwise you’ll get this completely worthless error message that tells you nothing about the problem.

Also, keep in mind that VS seems to cache the assembly so if you make any changes to it, you have to reload VS.