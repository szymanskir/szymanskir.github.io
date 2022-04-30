---
title: The Problem With DRY
author: 'Ryszard Szymański'
date: '2022-04-30'
slug: []
categories: []
tags: []
---


# What is the DRY principle about
DRY stands for *Don't Repeat Yourself* and is a heuristic that each software engineer will encounter at some point during their career. An example of using this advice is abstracting repetitive code chunks into functions in your program. Robert C. Martin in [Clean Code](https://www.goodreads.com/book/show/3735293-clean-code) even states that duplicate code is the *root of all evil*. In this post I want to argue that DRY can lead to more harm than good when used blindly. 

# My Problem With DRY
Don't get me wrong, DRY is good advice - you want to avoid obvious repetitions in your code. However, as with everything in software engineering, there are trade offs that we need to consider.

I remember when I was writing code for the purpose of automating some business processes. During the implementation I noticed that parts of those processes are similar to each other. Therefore, I applied the DRY heuristic and abstracted away those repetitions with the aim of improving the quality of my code. However, later it turned out that those similarities were purely coincidental and that at their core, those processes were completely different.

You can think of it as a [false equivalence](https://en.wikipedia.org/wiki/False_equivalence) like for example thinking that both a car and motorcycle have engines, therefore you drive them the same way. As a result of this mistake, I have fallen into the trap described by Sandi Metz in [this blogpost](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction) of creating the wrong abstraction. This can have greater consequences than a bit of code repetition. You might feel inclined to keep the wrong abstraction due to the [sunk cost fallacy](https://en.wikipedia.org/wiki/Sunk_cost), leading to further amplifying the incorrect abstraction and worsening your design. 

Kent Beck acknowledges that in [Test-Driven Development: By Example](https://www.goodreads.com/book/show/387190.Test_Driven_Development) and says *Duplication is always a bad thing, unless you look at it as motivation to find the missing design element*. Therefore, I believe that before blindly abstracting things away using DRY - you should ask yourself *Is this actually the right abstraction?*

Dave Farley in [this video](https://www.youtube.com/watch?v=cqKGDpnE4eY) described another potential problem of applying the DRY principle to a microservice architecture. Imagine that you have developed two microservices and you notice that some logic is duplicated in both of them. You might think that it is a good idea to extract those repetitions into a library that will then become a dependency used by both of the microservices. The problem here is that you introduce *coupling* between the two microservices. In case it is required to modify the library for the need of one microservice, the change impacts the second microservice as well. 

Now, you have found yourself in a situation where you wanted to apply a microservices architecture to make your microservices independent (to be able to develop and deploy them independently) and now because of the *coupling* the microservices are indirectly dependent on each other through the shared library.


# Summary
DRY is good advice, but applied unconsciously can cause more harm than good. Therefore, next time you bring up DRY in a code review as an *ultimate truth* - ask yourself whether applying it is actually going to be beneficial in this case.
