---
title: '''Scalability'' - What Do We Mean By That'
author: ''
date: '2024-06-09'
slug: []
categories: []
tags: []
---


I remember this job interview, me and the interviewer were talking about my experience in different programming languages. 

At one point we started talking about languages like R and Python and to my surprise the interviewer interrupted me and said *those languages do not scale*.

I was still relatively early in my career and it was not clear to me what they mean by that.

This term was very confusing for me. For example: one person says to just create static websites because they scale better, a different person says that you have to use Rust on the server side to get scalability. 

This can leave others confused as those seem to be two drastically different recommendations for the same *scalability issue*.

Each situation can be different and have their own scalability challenges. In this blog post I'd like to go through different examples to show multiple dimensions of *scalability*.
## Case 1: Handling Millions of Users

With scaling we often think about the amount of users our product is going to have.

To be honest, you can probably take most technologies and if you throw enough money into infrastructure resources, you should be good to go (assuming you have infinite money).

Conversely, you can take the fastest programming language, but if you don’t have enough infrastructure resources and you keep on adding users you will at some point reach a limit.

So I think handing millions of users is not the right problem statement. To be more specific I believe we should reframe the problem to:

*Handling millions of users at a cost that allows us to have a positive and meaningful Return On Investment*

And this brings us to case 2

## Case 2: Handling the Costs of Millions of Users

 Now we get more specific, which allows us to make more objective judgements.

Let’s assume that we are considering two technologies A and B.

To simplify the example let’s assume that 1 process running language A and 1 running language B consume the same amount of resources (CPU, RAM, etc.). 

But let’s say that 1 process of language A is able to handle 10 users while 1 process of language B is able to handle a 100 users. By *handling* I mean they are able to provide our expected User Experience (e.g. response times of a given magnitude).

Let’s assume our traffic is 1000 of users, we can handle that with 10 processes of language B and 100 processes of language A.

As each process consumes the same amount of resources we need 10x more resources for language A to handle the same traffic.

Because of that it will probably mean that the cost of running language A will be higher than language B (not necessarily 10x as the cost of resources may not be linear).

> One thing we did not take into account is the cost of development time.
> 
>  What if programmers of language B earn 10x more than programmers of language A and are harder to find?
>
> This means additional costs of employment and recruitment! Do they outweigh the savings on infrastructure costs? 
> We won't be diving deeper into that in this blog post, but it is another dimension to keep in mind.

## Case 3: Handling A LOT of Data

Static sites are a nice idea as the only thing our server needs to do is serve the static content and from that point everything else happens in the users browsers and consumes the resources of their devices.

It might work well if the data we use there is small and doesn’t change often. Let’s say a couple of MBs of data with which the user can interact with.

What if data gets bigger? Let’s say GB, Tb and Pb of data? Things probably won’t work, as the resources on the client device won’t be enough and you will be pushing large amounts of data through the network which can be slow and costly.

This means that suddenly our scalable static option is not that scalable anymore.

Now we need a different solution, servers or multiple servers that will allow us to handle the required amounts of data. This shifts our perspective on what we mean by scalability.

> We can go here into a bigger rabbit hole, we have a lot of data but what are our needs in terms of throughput and latency, which again is another dimension to consider.

## Case 4: Does the Tech Scale to Hundreds of Developers
As your codebase grows along with the amount of involved developers some issues might star to appear, e.g. slow compiling times or build times. 

Another dimension of scalability is whether many developers are able to collaborate in the source code?

Let’s say your project has a test suite that is growing over time. At some point your test suite is going to get large enough that it won’t be sustainable to run it for each code change.

There are different tools that can help with this issue like [Turborepo](https://turbo.build/) which will cache results of tasks allowing you to only run the tasks that need to be run.

If such tooling is not available in your language you might notice a slow down at some point when your codebase grows.
## Conclusions
Scalability is too general of a term to lead to meaningful discussions. 

To improve your scalability related discussions identify what dimensions are important in your context:
1. Are you worried about large infrastructure costs? When is it too expensive?
2. Are you worried about handling large amounts of data? How much data?
3. Are you worried about a large number of users? How many users do you expect?
4. Is it a combination of all the 3 above?

Not talking about those dimensions might lead to just picking *the supposedly more scalable solution* but not scalable in the sense that you are hoping for.