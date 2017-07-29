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
or [deadlock](https://en.wikipedia.org/wiki/Deadlock). Thus getting us linear speedup :-D. However until that day comes, programmers have to do that manually. That means relying on one of several threading libraries.

There are some like [Pthreads](http://man7.org/linux/man-pages/man7/pthreads.7.html) which are general purpose, but are low level. They are general purpose because they works for both [task level parallelism](https://en.wikipedia.org/wiki/Task_parallelism) and [data level parallelism](https://en.wikipedia.org/wiki/Data_parallelism).
There are some like [OpenMP](http://www.openmp.org) which are high level, but fits better for data level parallelism.

[Intel Threading Building Blocks](https://www.threadingbuildingblocks.org/) (TBB) fits the bill perfectly in that respect. It is both high level, where programmers do not need to do any low level thread management themselves. It works for both task level and data level parallelism.




<!-- ## Components ## -->
<!-- There are different components of TBB. -->

<!-- * Basic Algorithms -->
<!--   * [parallel_for]({% post_url 2016-10-06-intel-tbb-parallel-for %}) -->
<!--   * [parallel_reduce]({% post_url 2016-10-06-intel-tbb-parallel-reduce %}) -->
<!--   * [parallel_scan]({% post_url 2016-10-06-intel-tbb-parallel-scan %}) -->

<!-- * Advanced Algorithms -->
<!--   * [parallel_while]({% post_url 2016-10-06-intel-tbb-parallel-while %}) -->
<!--   * [parallel_do]({% post_url 2016-10-06-intel-tbb-parallel-do %}) -->
<!--   * [parallel_pipeline]({% post_url 2016-10-06-intel-tbb-parallel-pipeline %}) -->
<!--   * [parallel_sort]({% post_url 2016-10-06-intel-tbb-parallel-sort %}) -->

<!-- * Containers -->
<!--   * [concurrent_queue]({% post_url 2016-10-06-intel-tbb-concurrent-queue %}) -->
<!--   * [concurrent_priority_queue]({% post_url 2016-10-06-intel-tbb-concurrent-priority-queue %}) -->
<!--   * [concurrent_vector]({% post_url 2016-10-06-intel-tbb-concurrent-vector %}) -->
<!--   * [concurrent_hash_map]({% post_url 2016-10-06-intel-tbb-concurrent-hash-map %}) -->

<!-- * Atomic operators -->
<!--   * [compare_and_swap]({% post_url 2016-10-06-intel-tbb-compare-and-swap %}) -->
<!--   * [fetch_and_add]({% post_url 2016-10-06-intel-tbb-fetch-and-add %}) -->
<!--   * [fetch_and_decrement]({% post_url 2016-10-06-intel-tbb-fetch-and-decrement %}) -->
<!--   * [fetch_and_increment]({% post_url 2016-10-06-intel-tbb-fetch-and-increment %}) -->
<!--   * [fetch_and_store]({% post_url 2016-10-06-intel-tbb-fetch-and-store %}) -->

<!-- * Mutual exclusion -->
<!--   * [mutex]({% post_url 2016-10-06-intel-tbb-mutex %}) -->
<!--   * [spin_mutex]({% post_url 2016-10-06-intel-tbb-spin-mutex %}) -->
<!--   * [queueing_mutex]({% post_url 2016-10-06-intel-tbb-queueing-mutex %}) -->
<!--   * [spin_rw_mutex]({% post_url 2016-10-06-intel-tbb-spin-rw-mutex %}) -->
<!--   * [queuing_rw_mutex]({% post_url 2016-10-06-intel-tbb-queuing-rwr-mutex %}) -->
<!--   * [recursive_mutex]({% post_url 2016-10-06-intel-tbb-recursive-mutex %}) -->

<!-- * Memory allocation -->
<!--   * [scalabale_malloc]({% post_url 2016-10-06-intel-tbb-scalabale-malloc %}) -->
<!--   * [scallable_free]({% post_url 2016-10-06-intel-tbb-scallable-free %}) -->
<!--   * [scalable_realloc]({% post_url 2016-10-06-intel-tbb-scalable-realloc %}) -->
<!--   * [scalable_calloc]({% post_url 2016-10-06-intel-tbb-scalable-calloc %}) -->
<!--   * [scalable_allocator]({% post_url 2016-10-06-intel-tbb-scalable-allocator %}) -->
<!--   * [cache_aligned_allocator]({% post_url 2016-10-06-intel-tbb-cache-aligned-allocator %}) -->

