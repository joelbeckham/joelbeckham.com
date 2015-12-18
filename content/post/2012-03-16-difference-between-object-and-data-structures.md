---
title: Difference between object and data structures
author: jbeckham
layout: post
date: 2012-03-16
url: /2012/03/difference-between-object-and-data-structures/
categories:
  - Dev
---
I&#8217;ve been reading Clean Code by Robert C. Martin and really appreciated how he described the distinctions between objects and data structures:

> "**Objects** hide their data behind abstractions and expose functions that operate on that data. **Data structures** expose their data and have no meaningful functions."

> "**Object** expose behavior and hide data. This makes it easy to add new kinds of objects without changing existing behaviors. It also makes it hard to add new behaviors to existing objects."

> "**Data structures** expose data and have no significant behavior. This makes it easy to add new behaviors to existing data structures but makes it hard to add new data structures to existing functions."