---
title: Pessimistic vs Optimistic concurrency control
author: jbeckham
layout: post
date: 2012-03-16
url: /2012/03/pessimistic-vs-optimistic-concurrency-control/
categories:
  - DB
---
From <http://msdn.microsoft.com/en-us/library/ms189132.aspx> (emphasis mine)

**Pessimistic concurrency control**

> A **system of locks** prevents users from modifying data in a way that affects other users. After a user performs an action that causes a lock to be applied, other users cannot perform actions that would conflict with the lock until the owner releases it. This is called pessimistic control because it is mainly **used in environments where there is high contention for data**, where the **cost of protecting data with locks is less than the cost of rolling back transactions** if concurrency conflicts occur.

**Optimistic concurrency control**

> In optimistic concurrency control, users do not lock data when they read it. When a user updates data, the system **checks to see if another user changed the data** after it was read. If another user updated the data, an error is raised. Typically, the user receiving the error rolls back the transaction and starts over. This is called optimistic because it is mainly **used in environments where there is low contention for data**, and where the **cost of occasionally rolling back a transaction is lower than the cost of locking** data when read.