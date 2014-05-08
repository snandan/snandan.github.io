---
layout: post
title: Logistics of Software development
---

# What it takes to create a software
A developer, an editor, a compiler are not sufficient to create great softwares. There are lot of other things involved but not well talked about. For example, version control, build system, regression system and the precesses around them. Every software need support of them to be easily maintained. 

# Version Control
Version control does not mean that you throw Perforce or Git to the developers and you are done. They need to be configured for each teams requiment. Each software is unique - be its complexity, release schedule or customer engagement. Each software development team need to have the version control system configured for them. 
Branch management, integration of code across branches, culprit analysis, release management are each difficult problems to be solved by each developer seperately. There should be some carefully created automation system built around them. 
In a typical commercial software generally three to ten branches need to be maintained simultenously. Imagine the productivity loss a developer has to face, if he has to integrate the same fix in 10 different branches seperately. Besides, it is plain boring. 

I would center by thoughts around this problem in this post. How can code integration across branches be better automated and thereby have a better branch management system. 

# Automated code integration - what are the problems
Suppose you have created a system which would automatically takes a developers checkin and integrate them into all available branches. There are problems before and after this step. 

The problem before is that how would the system know whether to integrate the checkin into a particular branch? May be it is not needed in that branch. The developer is trying out a new feature in a development branch and that checkin should not go into a production branch.

If you think the answer to this problem is not to integrate anything from development branch to production branch, then read the following.
There can be cases where developer has fixed something which is critical to a customer. However instead of doing that in production branch, he has done that in the development branch and expects the auto-integration system to take care of the rest. Maybe he had to try 10 different things to reach to the actual fix, and hence he did not want to mess up in the production branch. 

So as it turns out, some external input is needed for the system to tell whether a particular fix is needed in a branch or not. We can ask the developer to answer that question. Hay buddy - you checked in something in 'master', tell me where else should it go.
That is a perfectly valid answer. This might work in lot of cases. However there is another problem to this. Developers, in cases, might not have answer to this question. He might not even know what all branches exist. This might seem too extreme - but that is true.

The problem after that is that integration may not go well as expected. There might be merge conflicts, or regression failures, or else, some dependecy which needs to be resolved before the checkin can go in. May be there is a prior checkin which needs to be integrated before the current checkin can go.

Fo each of this cases, we may inform the developer through some automated way (automatic email) and put the job into a queue. Unless the developer fixes that, the current checkin and all its dependent ones would not be considered for automatic integration.

# Dependency resolution between checkins 
There can be three type of dependencies in checkins. 
	- First one is if not resoleved would lead to a merge conflict. 
	  Maybe two developers or the same developer has changed same part of code in two different checkins.

	- The second one is where there is no merge conflict but resulted in a compilation error. 
	  This can happed when one developer changes a function signature, which another developer used.
	  
    - The third one is where compilation was successful, but which caused failures in regressions.
	  This is where compilation has passed, but introduced a logical error in the program. This can happen when based on the 
	  changes in the first checkin some more changes need to happed in the second checkin.
	  
Of the above three, the last one is the most time consuming and also dfficult to resolve. It needs to be resolved manually, there does not seem to any automatic process possible.

Anyway, all these make the dependency analysis between checkins all more useful.
