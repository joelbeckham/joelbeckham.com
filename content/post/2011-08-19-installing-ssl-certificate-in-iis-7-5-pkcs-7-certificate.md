---
title: 'Installing SSL Certificate in IIS 7.5 (PKCS #7 Certificate)'
author: jbeckham
layout: post
date: 2011-08-19
url: /2011/08/installing-ssl-certificate-in-iis-7-5-pkcs-7-certificate/
categories:
  - Dev
tags:
  - IIS
---
<div class="jive-rendered-content">
  <p>
    Wow&#8230; what a pain.
  </p>
  
  <p>
    If you have a .p7b certificate
  </p>
  
  <p>
    <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093208.gif"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="20110621093208" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093208_thumb.gif?resize=193%2C53" alt="20110621093208" border="0" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    that needs to be installed in IIS 7.5
  </p>
  
  <p>
    <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093236.gif"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="20110621093236" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093236_thumb.gif?resize=419%2C210" alt="20110621093236" border="0" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    You may receive this error, &quot;Cannot find the certificate request that is associated with this certificate file.&quot;
  </p>
  
  <p>
    <a href="http://i2.wp.com/img41.imageshack.us/img41/2978/20110621093301.gif"><img src="http://i2.wp.com/img41.imageshack.us/img41/2978/20110621093301.gif?resize=396%2C150" alt="" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    If that’s the case, here’s how to get the certificate installed.
  </p>
  
  <p>
    Start up certmgr.msc.
  </p>
  
  <p>
    <a href="http://i1.wp.com/img231.imageshack.us/img231/8639/20110621094322.gif"><img src="http://i1.wp.com/img231.imageshack.us/img231/8639/20110621094322.gif?resize=249%2C102" alt="" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    Right click on a folder –> All Tasks –> Import…
  </p>
  
  <p>
    <a href="http://i0.wp.com/img4.imageshack.us/img4/5947/20110621093412.gif"><img src="http://i0.wp.com/img4.imageshack.us/img4/5947/20110621093412.gif?resize=388%2C222" alt="" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    Import the .p7b certificate.
  </p>
  
  <p>
    <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093444.gif"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="20110621093444" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093444_thumb.gif?resize=444%2C233" alt="20110621093444" border="0" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    Select &quot;Automatically select a certificate store&quot;
  </p>
  
  <p>
    <a href="http://i1.wp.com/img860.imageshack.us/img860/6696/20110621093506.gif"><img src="http://i1.wp.com/img860.imageshack.us/img860/6696/20110621093506.gif?resize=500%2C250" alt="" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    It’ll be imported under Personal –> Certificates (you may need to refresh).
  </p>
  
  <p>
    <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093532.gif"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="20110621093532" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093532_thumb.gif?resize=507%2C127" alt="20110621093532" border="0" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    Right click on the certificate –> All Tasks –> Export.
  </p>
  
  <p>
    <a href="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093607.gif"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="20110621093607" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093607_thumb.gif?resize=336%2C174" alt="20110621093607" border="0" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    Export as &quot;DER encoded binary X.509 (.CER).&quot;
  </p>
  
  <p>
    <a href="http://i0.wp.com/img87.imageshack.us/img87/2010/20110621093629.gif"><img src="http://i0.wp.com/img87.imageshack.us/img87/2010/20110621093629.gif?resize=501%2C210" alt="" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    Give it a filename.
  </p>
  
  <p>
    <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093656.gif"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="20110621093656" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093656_thumb.gif?resize=461%2C165" alt="20110621093656" border="0" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    Back in IIS, repeat the process for completing the certificate request. This time give it the .cer file you just exported.
  </p>
  
  <p>
    <a href="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093729.gif"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="20110621093729" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2011/08/20110621093729_thumb.gif?resize=454%2C191" alt="20110621093729" border="0" data-recalc-dims="1" /></a>
  </p>
  
  <p>
    That should install the certificate.
  </p>
</div>