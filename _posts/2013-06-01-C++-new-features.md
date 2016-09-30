---
layout: post
title: C++ new language features
comments: true
---

# Introduction #
The new [C++ standard](http://www.stroustrup.com/C++11FAQ.html) has brought in lot of new features in the language. A lot of there features if used properly can make the code a lot cleaner.
In this post I will try to capture the features I find most useful.

## Auto  ##
The new standard takes away the responsibility to put the type in the
'lhs' of an expression, if the type can be deduced from the 'rhs'.

For example in C++ '98 we need to write:

{% highlight c++ %}
void func (const vector<int>& intVec) const
{
	vector<int>::const_iterator iter = intVec.begin();
	for (; iter != intVec.end(); ++iter) {
		// rest of the code
	}
}
{% endhighlight %}

The same code can be written using the 'auto' feature in the following
way:

{% highlight c++ %}
void func (const vector<int>& intVec) const
{
	auto iter = intVec.begin();
	for (; iter != intVec.end(); ++iter) {
		// rest of the code
	}
}
{% endhighlight %}

## Lambda functions ##

## Rvalue reference ##

## Move sementics ##

## Non member begin() and end() ##

## Initializer list ##

## Smart pointers ##

## nullptr ##

## New syntax for 'for' ##


