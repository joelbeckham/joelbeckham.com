---
title: Update from Select with Join
author: jbeckham
layout: post
date: 2011-10-14
url: /2011/10/update-from-select-with-join/
categories:
  - DB
---
I always forget the syntax for doing an update from a select:

<pre style="width: 577px; height: 288px"><code>
UPDATE
    Table
SET
    Table.col1 = other_table.col1,
    Table.col2 = other_table.col2
FROM
    Table
INNER JOIN
    other_table
ON    Table.id = other_table.id
</code></pre>