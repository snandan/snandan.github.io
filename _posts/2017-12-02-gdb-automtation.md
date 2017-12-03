---
layout: post
title: Offline Debug in GDB
tags: [gdb]
comments: true
type: post
published: true
meta: {}
---

## TL;DR
Instead of writing 'step', 'next' and 'continue' in GDB, is there any better way to debug long running processes? Yes, you can use offline mode. It is not a panecea, but it can ease your life in lot of situations.

## Introduction
Generally developers use [GDB](https://en.wikipedia.org/wiki/GNU_Debugger) in _online_ mode, i.e. start GDB and run the misbehaving program through it. Put breakpoints and when the program hits any of the breakpoints, get/set value of variables, step through the execution etc. This is a very convinient way of finding out issues. However it can become a problem when it hits a breakpoint thousands of time during the course of execution which runs for hours and for most of the cases the program runs as expected - only a few times it shows the error condition.

In such cases it is sometimes better to run GDB in _offline_ mode. GDB offers a rich set of features where one can set breakpoints and set tasks to be executed when the breakpoints are hit. Not only that, it is possible to log the entire session of GDB into a file. 
What we want is to run GDB along with the program in batch mode and then post process the GDB log file to figure out what was the problem.

Let me demostrate that with a very simple example.

## Example
I am using the following C++ program for my illustration:

{% highlight c++ %}
// test.cpp

#include <iostream>
#include <vector>
int func(int inp)
{
    return inp + 1;
}
int main()
{
    std::vector<int> vec = {12, 45, 24, 2, 16 };

    for (int i = 0; i < 5; i++) {
        int retval = func (vec[i]);
    }
}

{% endhighlight %}

Compile it with debug symbols enabled.

{% highlight shell %}
$ g++ test.cpp -g -std=c++14
{% endhighlight  %}

Next step is to create the automation script for gdb.
GDB by default paginate screen output by default. Once a screen is filled with output, it halts and asks user whether to proceed to dump more output or quit. 

We do not need this behavior to interfare with our batch mode execution.
So in the gdb script file, we turn off pagination as the first thing.

{% highlight sh %}
#
# gdb.script
#

# Do not wait to hit enter on every page scroll
set pagination off
# set up logging
set logging on

# Load the executable
file a.out

# Set breakpoint on function 'func'
b func

# Set of commands to run after hitting the breakpoint
# In this case, just print the stacktrace and continue the run.
commands
backtrace
continue
end

# Run the program
run

# Clean up..
set logging off
quit

{% endhighlight %}

Next we set logging on. The default name of output log file which GDB creates is *gdb.txt*.
We load the executable and set the breakpoint in function 'func'. 

Next comes the interesting part. Any command specified between 'commands' and 'end' are executed on hitting the **last** breakpoint set. The official help from GDB is lot more informative.

{% highlight sh %}
(gdb) help commands
Set commands to be executed when a breakpoint is hit.
Give breakpoint number as argument after "commands".
With no argument, the targeted breakpoint is the last one set.
The commands themselves follow starting on the next line.
Type a line containing "end" to indicate the end of them.
Give "silent" as the first line to make the breakpoint silent;
then no output is printed when it is hit, except what the commands print.
{% endhighlight %}

In our case, it prints the *backtrace* and just *continue* the execution on hitting the breakpoint set on function 'func'.
You can write any number of GDB commands here.

Then run the program and once it finishes, set logging off and quit from GDB.

Run the program in GDB like the following. If it is a long running program then feel free to make use of that time (grab a coffee and go out for a walk maybe).

{% highlight sh %}
$ gdb a.out
(gdb) source gdb.script
{% endhighlight %}

Anyway, for this simple example, I get the following output in the *gdb.txt* file.

{% highlight gdb %}
$ cat gdb.txt
Breakpoint 1 at 0x1000012f7: file test.cpp, line 6.
[New Thread 0x1403 of process 16280]
warning: unhandled dyld version (15)

Thread 2 hit Breakpoint 1, func (inp=12) at test.cpp:6
6	    return inp + 1;
#0  func (inp=12) at test.cpp:6
#1  0x000000010000152c in main () at test.cpp:15

Thread 2 hit Breakpoint 1, func (inp=45) at test.cpp:6
6	    return inp + 1;
#0  func (inp=45) at test.cpp:6
#1  0x000000010000152c in main () at test.cpp:15

Thread 2 hit Breakpoint 1, func (inp=24) at test.cpp:6
6	    return inp + 1;
#0  func (inp=24) at test.cpp:6
#1  0x000000010000152c in main () at test.cpp:15

Thread 2 hit Breakpoint 1, func (inp=2) at test.cpp:6
6	    return inp + 1;
#0  func (inp=2) at test.cpp:6
#1  0x000000010000152c in main () at test.cpp:15

Thread 2 hit Breakpoint 1, func (inp=16) at test.cpp:6
6	    return inp + 1;
#0  func (inp=16) at test.cpp:6
#1  0x000000010000152c in main () at test.cpp:15
[Inferior 1 (process 16280) exited normally]
{% endhighlight %}

Now we can postprocess the *gdb.txt* file to figure out whats wrong with the program. By the way, there is nothing wrong with this program. It is too trivial to have any problem. But other programs I write, have lots of them.

I believe this gives some insight regarding how to use GDB in _offline_ mode.
