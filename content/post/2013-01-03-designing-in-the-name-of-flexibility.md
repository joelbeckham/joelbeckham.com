---
title: Designing in the name of "flexibility"
author: jbeckham
layout: post
date: 2013-01-04
url: /2013/01/designing-in-the-name-of-flexibility/
categories:
  - Dev
---
Oh man, the post, [Winning is the worst thing that can happen in Vegas][1], names and calls out a tendency of which I've gradually been gaining self-awareness.

> Future coding is a lot like playing the roulette. If you can guess where the requirements of tomorrow will land today, you've just scored the ultimate programmer’s prize: looking like a wizard. You saw the future and you were right! High five, brain!
> 
> That’s the almost irresistible draw of &quot;flexibility&quot;—often just a euphemism for building half or whole features before you know how they’re supposed to work or whether you need them. Just like in Vegas, the worst thing that can happen is to be right about this once in a while.

&nbsp;

Relating to technical debt:

> Running up the debt on your code is not just about the quick hacks and dirty commits you know you really should clean up (but just don’t). No, the far more insidious kind of debt is that acquired in the name of &quot;flexibility&quot;.

&nbsp;

Equating this to technical debt never crossed my mind before but really resonates with me. Before hearing this talk, I had been thinking a lot about the role of code comments. Over this past year my conviction that comments bring more of a liability than benefit 99% of the time has been deepening. They take time to write (which could be spent on writing clearer code to begin with), and when they aren't maintained (which seems to happen a lot), the code is much harder to understand than if there were no comments at all. It's not much of a leap for me to agree that coding for unknown future requirements is a bad thing. It becomes a liability that must be understood and maintained and rarely outweighs the benefits of getting it right once in a while.

 [1]: http://37signals.com/svn/posts/3384-winning-is-the-worst-thing-that-can-happen-in-vegas