---
layout: post
title: 3 important lessons before using Intel TBB
tags: intel tbb
comments: true
---

## Introduction ##
Intel Threading Building Blocks (TBB) does a nice job by abstracting away all the thread management related work.
Users just need to concentrate on the breaking the work into individual tasks which can run parallely - preferably without causing any synchronization issue. 
It is possible to explicitly sychronize using various types of mutexes supplied by TBB - but that comes later.

In this post, I will try to explain the various concepts needed to start using Intel TBB effectively.

## Blocked Range ## 
