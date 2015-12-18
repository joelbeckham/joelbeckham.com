---
title: 'TeamCity & Beanstalk: bad_record_mac'
author: jbeckham
layout: post
date: 2012-06-01
url: /2012/06/teamcity-beanstalk-bad_record_mac/
categories:
  - Build Automation
  - Dev
tags:
  - TeamCity
---
I started getting __bad\_record\_mac__ errors when TeamCity would try to connect to our SVN repository hosted on beanstalkapp.com. Here is the fix:

  * From command prompt, run
  * c:teamcitybintomcat7w.exe //ES//TeamCity
  * Click the &#8220;Java&#8221; tab
  * Add the following to Java Options:
  * -Dsvnkit.http.sslProtocols=SSLv3
  * Restart the teamcity service

From: <http://devnet.jetbrains.net/thread/434355;jsessionid=D5DF978AB09E2CD1E16F9C8B65482E94?tstart=-2>