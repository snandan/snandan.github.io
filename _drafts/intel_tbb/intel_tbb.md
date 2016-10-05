---
layout: post
title: Intel Threading Building Blocks
comments: true
---

## Introduction ##
Ever since processer makers [stopped increasing CPU speed but started putting more cores](http://www.extremetech.com/computing/116561-the-death-of-cpu-scaling-from-one-core-to-many-and-why-were-still-stuck),
there had been a pressing need for application developers to use them to make programs run faster. However that is easier said then done.
This [blog post](http://blog.smartbear.com/programming/why-johnny-cant-write-multithreaded-programs/) points out the same fact in an interesting way.
It would be great if compilers can take any code and generate executables which can run on any number of cores parallely without any [race condition](https://en.wikipedia.org/wiki/Race_condition#Software)
or [deadlock](https://en.wikipedia.org/wiki/Deadlock). Thus getting us linear speedup :grimacing:. However until that day cores, programmers have to do that manually. That means relying on one of several threading libraries.

There are some like [Pthreads](http://man7.org/linux/man-pages/man7/pthreads.7.html) which are general purpose, but are low level. They are general purpose because they works for both [task level parallelism](https://en.wikipedia.org/wiki/Task_parallelism) and [data level parallelism](https://en.wikipedia.org/wiki/Data_parallelism).
There are some like [OpenMP]() which are high level, but fits better for data level parallelism.

[Intel Threading Building Blocks](https://www.threadingbuildingblocks.org/) (TBB) fits the bill perfectly in that respect. It is both high level, where programmers do not need to do any low level thread management themselves. It works for both task level and data level parallelism.


## Components ##
There are different components if TBB.

* Basic Algorithms
  * [parallel_for]()
  * [parallel_reduce]()
  * [parallel_scan]()

* Advanced Algorithms
  * [paralllel_while]()
  * [parallel_do]()
  * [parallel_pipeline]()
  * [parallel_sort]()

* Containers
  * [concurrent_queue]()
  * [concurrent_priority_queue]()
  * [concurrent_vector]()
  * [concurrent_hash_map]()

* Atomic operators
  * [compare_and_swap]()
  * [fetch_and_add]()
  * [fetch_and_decrement]()
  * [fetch_and_increment]()
  * [fetch_and_store]()

* Mutual exclusion
  * [mutex]()
  * [spin_mutex]()
  * [queueing_mutex]()
  * [spin_rw_mutex]()
  * [queuing_rw_mutex]()
  * [recursive_mutex]()

* Memory allocation
  * [scalabale_malloc]()
  * [scallable_free]()
  * [scalable_realloc]()
  * [scalable_calloc]()
  * [scalable_allocator]()
  * [cache_aligned_allocator]()

