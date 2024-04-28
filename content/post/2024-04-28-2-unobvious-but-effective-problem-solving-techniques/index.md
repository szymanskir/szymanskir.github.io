---
title: 2 Unobvious But Effective Problem Solving Techniques
author: ''
date: '2024-04-28'
slug: []
categories: []
tags: []
---


As a software engineer, most of my time is spent on solving different kinds of problems. These problems are not necessarily always technical in nature.

Sometimes instead of solving the problem, you can find a solution that doesn’t necessarily involve resolving the issue directly.

In this post I’d like to share two techniques that allow you to do that.

## Technique 1: Reframing the Problem

Sometimes when we are asked to solve the problem, the problem statement might be incorrect.

Or the statement is made in such a way that narrows down the possible landscape of solutions.

A good example of such problem statement is: 

> *We have 4 features to implement and a deadline in a month. How many people do we need to add to the project to complete those 4 features in that time?*

This problem statement forces you to think in terms of solutions of the type: *I can add from 0 to 10 developers to the team*.

What if we looked at the problem from other angles. For example: 

> *Why do those 4 features need to be implemented until that deadline? Is it a regulatory requirement or is it just a manager who would love to have those features at that time?*

Let’s assume for the sake of the example that it’s a regulatory requirement and if we don’t address it until that deadline, we will get fined.

Now we know that that the deadline part of the problem statement can be hard to reframe.

Let’s have a closer look at the 4 required features. Are all those 4 features required to meet regulatory requirements?

If not and only 2 are needed we can already reframe the problem to: 

> Are we able to implement those 2 features until that deadline.

We can also have a closer look at the complexity of those features - can we make them simpler to implement, but meet regulatory requirements at the same time?

A good example of simplifying a feature is the feature of collaborative editing. The solution can vary in terms of complexity:

1. More complex option: be able to write simultaneously in a doc in real time
2. Less complex option: only allow a single user to edit a document at the time and other users are able to view the doc in read mode

While of course option no 2 can be considered worse UX wise, it gives us a simpler solution to a similar problem which might actually be a enough in specific situations.

Now we can reframe the original problem statement to statements like:

> 1. What are the regulatory requirements that we need to meet by this deadline?
> 2. What is the simplest effective approach to meeting the regulatory requirements? 

And now we suddenly look at the same situation from different angles. Those different angles encourage us to explore new, potentially better solutions.

## Technique 2: Make the Problem Disappear

Sometimes a problem is caused by an upstream problem. In those cases, solving the upstream problem makes the downstream problem disappear. 

Let’s say you start using a new library that you find very useful. Over time you notice that the library is incompatible with other libraries you would like to use. This sparks problems.

you could solve the compatibility issues by patching the involved libraries to make them compatible

or

you could stop using the library that's the source of most compatibility issues

It comes down to your perceived ROI of that library - does it provide enough benefits to justify the costs of solving compatibility issues?

## Conclusion
Solving problems is just the tip of the iceberg. Solving the right problem is where we can find more value.

That’s why using techniques like *Reframing the Problem* or *Making the Problem Disappear* can be very powerful.

They allow us to look at the problem from different perspectives and pick the right problems to solve or come up with more effective solutions.

These 2 techniques are not mutually exclusive as reframing a problem might lead us to discovering an upstream problem. We can then solve that upstream problem to make the downstream problem disappear.