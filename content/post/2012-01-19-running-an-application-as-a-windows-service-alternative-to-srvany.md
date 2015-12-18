---
title: Running an application as a windows service (Alternative to srvany)
author: jbeckham
layout: post
date: 2012-01-19
url: /2012/01/running-an-application-as-a-windows-service-alternative-to-srvany/
categories:
  - Server
tags:
  - Windows
---
Until recently, when I wanted to set up a non-service application to run as a windows service, I always used srvany.exe. One of the problems with srvany is that it can’t detect if the application has crashed and therefore continues to&#160; report that it is still running. Since it doesn’t know when the application stops, the service manager doesn’t know to attempt to restart it.

In its place, I’ve started using a utility called [nssm.exe][1] (Non-Sucking Service Manager) and have had a lot of success. It’s just as easy to set up as srvany, but works a lot better.

Detailed Usage Instructions here: <http://nssm.cc/usage>

Once you install the service, you can edit additional properties, such as setting the working directory (AppDirectory), by editing the service settings in the registry. Navigate to HKEY\_LOCAL\_MACHINESYSTEMCurrentControlSetServices<Service Name>Parameters

 [1]: http://nssm.cc/