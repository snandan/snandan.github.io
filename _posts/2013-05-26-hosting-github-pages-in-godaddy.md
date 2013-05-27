---
layout: post
title: Hosting Github Pages in Go-Daddy.com
---

[GitHub](https://github.com) has done a great job by providing a free blogging platform through GitHub Pages. 
There are two types of blogs supported by GitHub at present. First one targetted to particular projects called 'Project Pages'. 
The second one targetted to Github users, individuals or organizations called 'User and Organization Pages'. 
The GitHub official documentation can be found [here](https://help.github.com/categories/20/articles).

In this post, i will describe only about 'User and Organization Pages'. 
There are some differences in setting up 'Project Pages' - that I would describe in some other post if neccessary. 

To create a 'User and Organization Page' (I would stick to 'page' for the rest of the post) one has to create a repository in GitHub
with the following name '**username**.github.io'. There should be an 'index.html' file in the root. The rest are all HTML/CSS/JS stuff as 
one wants to configure the content and look-and-feel.

The blog gets hosted and get the URL as: **username**.github.com.

However if someone wants to host in a custom domain, he needs to get a domain name registered via [Go-Daddy](https://www.godaddy.com) or some other domain name registerer services. I did it through [Go-Daddy](https://www.godaddy.com).

Once that is done, one needs to do two things: 
1. Create a file called 'CNAME' and put that in the blog root, in github repository. The content of the 'CNAME' file is just the new domain one is interested in.
2. In the domain management page of [Go-Daddy](https://godaddy.com) add two records of type 'A' to point to the magic IP *204.232.175.78*.

After that, one has to wait for some time for DNS to take effect. Th waiting time can range from a few minutes to even hours.

You can check my repository [snandan.github.io](https://github.com/snandan/snandan.github.io) for reference.
