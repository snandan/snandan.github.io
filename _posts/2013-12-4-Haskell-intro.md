---
layout: post
title: Introduction to Haskell
tags: []
status: publish
type: post
published: true
meta: {}
---


I had been trying to learn functional programming for some time
now. Last time, my effort two years ago, failed kind of in a miserable
way. I tried too many things at once, Haskell, Scheme, Clojure all
together. This time I am focusing only on Haskell. People says a lot
about this language - its supposed to bend minds. Nothing of that sort
happened as of yet. That said - who knows, I have just started on it.
Haskell, no doubt is a very different language; a lot
different than the one I use in my day job.  Apart from its syntax,
the fundamental difference I found is that the language is 'lazy',
i.e. the statements do not get executed unless absolutely
needed. Other fundamental difference is that the language is "purely
functional" - i.e. like a function in mathematics, function in Haskell
can only produce results on given arguments. It does not do anything
else, even print a message unless arm twisted by the developer using
some advanced feature in the language called Monads (IO Monads to be
particular). What is a Monad? That is another story - worth another
post. Since the language is 'lazy' different surprising things can be
done in this language, like creating 'infinite' data-structures.  I
hope you need an example at this point to make things clear. Here it
goes: I list in Haskell can be written like this:

{% highlight haskell %}
ghci> let a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
{% endhighlight %}
This means 'a' is a list of ten numbers, 1 to 10. This can
concisely be written as the following:
{% highlight haskell %}
ghci> leta = [1..10]
{% endhighlight %}
This is same the the above.  However in Haskell
allows us to write the following:
{% highlight haskell %}
ghci> let a =[1..]
{% endhighlight %}
This is an infinite list of numbers starting from
1. Please do not try to print it. It will continue to print infinite
stream of numbers and you would need to manually abort the run.  You
may now ask what is the use of such structure and that would be a
totally valid question.  You can use it something like this:
{% highlight haskell %}
ghci> let a = [1..]  ghci> take 3 a [1, 2, 3]
{% endhighlight %}
The function 'take' number of elements as specified by the
first argument from the second argument which is a list. In this
example the first three items are taken and the rest are discarded,
not even calculated. This may seem to be a lame example (why not use
just 'a = [1, 2, 3]' instead). I do not disagree with you regarding
the example. But trust me, infinite data structures can be of huge
advantage lot of times.  In Haskell, we do not need to tell how to
calculate - rather we need to clearly tell what the problem statement
is. And sometimes that is the harder part.  For an example let us try
to find all the Pythagorean triplets occurring between 1 and 20. In
Haskell we can write it like the following
{% highlight haskell %}
ghci>[(a, b, c) | c <-[1..20], b <- [1..c], a <- [1..b], c^2 == a^2 + b^2]
[(3, 4, 5), (6, 8, 10), (5, 12, 13)]
{% endhighlight %}

Another interesting example which shows the power of Haskell is the
quicksort algorithm.
{% highlight haskell %}
qsort [] = [] qsort (x:xs)
         = qsort smaller x ++ [x] ++ qsort larger x
                 where smaller x =[a | a <- xs, a <= x]
                 larger x = [a | a <- xs, a > x]
{% endhighlight %}
Let's see, how the above example works.  The above quicksort algorithm is
recursive. The first line is the base condition. It says, qsort on an
empty list results in an empty list. The start of the second line
rescribes qsort on a non-empty list denoted by (x:xs). Lists in
Haskell are denoted a lot of times using that notation. This means the
first item in the list is 'x' and the rest of the items in the list is
'xs'. e.g. if we have list (x:xs) = [1, 2, 3, 4, 5] then x = 1, xs =
[2, 3, 4, 5] qosrt on a non-empty list is the concatenation of three
elements, the first one is the sorted list of items lesser than 'x',
the second item is 'x' itself and the third item is sorted list of
items greater than 'x'. I hope now you can appreciate how the
algorithm has been described so succinctly. I my other posts I will
describe some more regarding Haskell. Audios!
