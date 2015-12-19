---
title: 'SPF, Sender-ID, Domain Keys, DKIM, DMARC - Yikes!'
author: jbeckham
layout: post
date: 2012-03-20
url: /2012/03/spf-sender-id-domain-keys-dkim-dmarc-yikes/
categories:
  - Dev
tags:
  - Email
---
_<font color="#666666">(This is going to be a slowly evolving document as I have time to learn more about this)</font>_

****

**<a href="http://www.openspf.org/" target="_blank">SPF</a> _(Sender Policy Framework)_** - domains add a DNS TXT or newer, SPF, record which enumerates which mail servers are allowed to send mail on their behalf. They also can indicate what the recipient should do with mail not coming from one of the listed mail servers.

Pros: Simplicity. Can be implemented in a few minutes.

Cons: Spammers can just use their own domains which they then authorize themselves, or use accounts on trusted domains (like large webmail providers). Can be difficult for travelers sending corporate email through other relays. Doesn't provide any feedback as to whether it is working or not. Doesn't work with forwarded email &#8212; it only verifies the immediate sender.

Tools: <a href="http://www.kitterman.com/spf/validate.html" target="_blank">Verify SPF</a>

**DKIM _(Domain Keys Identified Mail)_** - The message envelope and original sender are signed with a private key. The public key is stored in the DNS record. The message isn't encrypted so that none-DKIM recipients can still read it.

Pros: The original sender can be verified and the message contents can be verified to be unchanged.

Cons: Complexity as each email needs to be signed. Doesn't provide any feedback as to whether it is working or not.

Tools: <a href="http://dkimcore.org/c/keycheck" target="_blank">Verify DKIM</a>

<a href="http://www.dmarc.org/" target="_blank"><strong>DMARC</strong></a> **_(Domain-based Message Authentication, Reporting, and Conformance)_** - gives SPF and DKIM users the ability to recommend policies to those receiving mail claiming to be from their domains, and to get back reports from compliant sites about mail from their site. It doesn't report on what the users does, but reports on the results of the SPF and DKIM checks and the kind of mail that has been received claiming to come from the sending domain. It uses a DNS TXT record.

<a href="www.microsoft.com/senderid" target="_blank"><strong>Sender-ID</strong></a> **-** Based on SPF with a few additions. SPF only verifies the MAIL FROM address (envelope sender) and not any of the other header addresses that indicate the sending party. Sender-ID defines a "Purported Responsible Address (PRA)" with a set of heuristic rules to establish this address from the many typical headers in an email.

Cons: Usually only offers protection when the email is legitimate.

<a href="http://en.wikipedia.org/wiki/Sender_ID" target="_blank">Wikipedia</a>

Domain Keys - is the branded name created by Yahoo. Because of licenseing issues, the community created DKIM which is very similar in response.

<http://www.extremetech.com/computing/117267-diving-into-dmarc-can-it-really-end-spam-or-at-least-phishing/2?print>