---
title: Copy / Pasting text into the Android Emulator
author: jbeckham
layout: post
date: 2011-09-01
url: /2011/09/copy-pasting-text-into-the-android-emulator/
categories:
  - Dev
---
I usually send the text I want to copy as an sms message through telnet and then copy the text from the sms message. Here&#8217;s how:

Connect through telnet:

  * **Syntax:** `telnet localhost <port>`
  * **Example:** `telnet localhost 5554`

_(5554 is the default port. The title bar of the emulator shows the port that is being used, so you can see if it&#8217;s different)._

Send message:

  * **Syntax:** `sms send <senders phone number> <message>`
  * **Example:** `sms send 1231231234 This is the message you want to send`

_(You can just make up the senders phone number)_

This works really well for links as the message is automatically converted into a hyperlink which you can click without having to copy / paste it into the browser.

Once the emulator receives the message you can copy it and paste it wherever you like.