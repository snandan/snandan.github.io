---
layout: post
title: Shannon Entropy and Information Gain
tags:
- Machine Learning
- Machine learning
status: publish
type: post
published: true
meta: {}
comments: true
---
Shannon Entropy and Information gain are some fundamental concepts used in classification algorithms like decision tree in machine learning. But before going deep into that let us first define **what is information**. Well, in a very crude sense information is the *number of bits* needed to represent a particular amount of data.

## Information Gain ##
Let us say someone wants to crack a password. All he knows is that the password in five character long and contains letter from English alphabet only - there are no digit or special characters in that. He has $$ 5^{26} $$ options to choose from. If he wants to put all those choices into a file or something, he would need some $$\large{A}$$ number of bits for that. Now lets say somehow he manages to find that the first two characters are 'g' and 'j'. The number of options for him now reduces to $$ 3^{26}$$. Let us say he would need $$ \large{B}$$ number of bits to represent that. The total number of bits needed by him now is $$ \large{B}$$ plus some bits to represent 'g' and 'j'. Since the last value is very small we can ignore that for the most part.

Obviously $$ \large{B}$$ is smaller than $$ \large{A}$$. We define the difference $$ \large{A} - \large{B}$$ as the information gain for this example. That is the number of bits he has saved by having that knowledge.
<p>
More formally we can define Information Gain as the following: Let \(\textbf{X} = (X, p)\) be a probability space. The information gain \(Gain (\textbf{Y}|\textbf{X})\) is the gain obtained by the knowledge that the outcome of an experiment belongs to a set \(\textbf{Y}\) where \(\textbf{Y} \subset \textbf{X}\)
</p>
<p style="text-align:center;">
$$ Gain(\textbf{Y}|\textbf{X}) = \log_2{p(\textbf{X})} - \log_2{p(\textbf{Y})} = \log_2{\frac{p(\textbf{X})}{p(\textbf{Y})}} = \log_2{\frac{1}{p(\textbf{Y})}} = - \log_2{p(\textbf{Y})} $$ 
</p>
## Shannon Entropy ##
Entropy is defined as the messiness or disorderliness or data. The primary goal of any classification algorithm is to split the data into subsets so that the messiness in each individual group reduces and thus reducing  the overall messiness. In other words the primary goal of any classification algorithm is to reduce the entropy of the data.

Shannon entropy is a mathematical model which can describe the disorderliness of a particular dataset. It is defined as

<p style="text-align:center;">
$$ H (\textbf{A}) = - \sum_{i=1}^{n} p_{i}\log_2{p_{i}} $$
</p>
