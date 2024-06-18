---
title: 3 Heuristics I Use To Avoid Over-engineering
author: ''
date: '2024-06-17'
slug: []
categories: []
tags: []
---

I remember early in my career when I would get finished with a feature I would seek out feedback from more senior colleagues.

I would usually ask - what they think about it and *looks good* usually was not enough for me. I would follow up with *could this be done better*. Interestingly, they often didn’t really have much additional feedback, which was frustrating as I wanted to get better.

However, this mindset of *constantly trying to improve things* would lead me to the following situation:
1. I would work on a feature
2. I would learn about a new concept (for example design patterns)
3. I would look for ways to apply the new concepts to my current work

This loop of learning about new things and trying to apply them to ongoing work would repeat itself multiple times leading to …

...you guessed it - over-engineering. I would blindly apply patterns without necessarily thinking if they are adding any value to the solution or taking into account  that they are adding complexity (as other developers would need to get acquainted with those patterns to understand my solution).

Over the years I managed to learn a couple of heuristics that prevent me from going down the over-engineering rabbit hole.
## Heuristic 1: Make Sure That The Problem You See Is An Actual Problem
When implementing your code, you are probably thinking about edge cases that you need to cover.

Sometimes you might notice additional business cases or you might try to anticipate future feature requests. While this is a good thing that you notice those, it’s not necessarily a good idea to try to handle them.

That’s why I always confirm if a business case I discovered is actually something I need to worry about. That way you avoid implementing additional code (thus adding complexity) for irrelevant cases.

## Heuristic 2: Start With The Simplest Solution And Build From It
My over-engineering mistake was trying to use new concepts I learned immediately.

Now, I try to make my solutions driven by the problem. For example, let’s say users of the app need to save things.

I start with the simplest case: I only have 1 user, so maybe I can just save their work in a file.

But what if I can have multiple users? I confirm that this is indeed a problem, if yes, then my solution with just dumping things to a file doesn’t work anymore.

So in this case, the simplest solution I can think of is using a database. The simplest option for me is using SQLite.

> Note: *by simplest for me* I want underline that this is subjective. Your skills and experience are a decisive factor e.g. if you know Java then it will probably be easier and faster for you to setup an API with Spring compared to using Django.

But is SQLite enough? We were talking about multiple users: does that mean multiple writers? If yes, then [SQLite might not be a good fit](https://www.sqlite.org/cgi/src/doc/begin-concurrent/doc/begin_concurrent.md). 

What’s the next simplest option? Well in my case it’s using PostgreSQL. Would it be enough?

What if I get millions of users and the write volume starts to be too high? Let’s assume in this example that we are working on an internal application and that the company has 50 employees. 50 is less than millions so it’s a case we probably don’t need to worry about.

With this iterative approach we came up with the simplest solution that solves our current problems and we avoid picking a solution that involves unnecessary complexity.

Some of you might wonder - but what if the company decides to make the app public, wouldn’t it be a disaster?

Well if this happens we still need to get to millions of users. And in that case I’d say - let’s get to that problem first and only if we start seeing a higher risk of this happening, let's take care of it. 

There are other ways to manage this risk, e.g. you could ask for a sign up list if you are worried about your product going viral, failing to scale and making a bad impression. That way you can estimate the initial interest and see how high the risk is.

## Heuristic 3: A Working Solution Is Better Than An Uncertain Better Solution
Sometimes when finishing a feature you might see ways of improving it.

But that feeling shouldn’t prevent you from shipping a working solution. Especially as implementing the improvements is an unknown (as long as it’s not ready we don’t know how long it will take to implement them).

In those cases I would usually opt-in to ship something earlier and chances are it will be good enough and further improvements (and the complexities that may come with it) won’t be worth the investment.

> **Note:** Of course at the same time, this does not mean we shouldn’t  pursue improvements. What I mean here is that the pursuit of improvements shouldn’t prevent shipping existing, working solutions.


## Summary
I used to over-engineer my solutions thinking that I was making them better.

Now to avoid doing that:
1. I make sure that the problem I see is a problem that needs to be solved
2. I start from the simplest solution and build from it
3. I prefer existing working solutions from uncertain better solutions