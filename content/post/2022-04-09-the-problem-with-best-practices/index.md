---
title: The Problem With Best Practices
author: 'Ryszard Szymański'
date: '2022-04-09'
slug: []
categories: []
tags: []
---

# Introduction
*Best Practices* is a term that I encounter often as a software engineer. Code reviews would be the situations where I would encounter the term most often, for example a colleague suggesting to do things differently and when asked about the advantages of their solution they would reply that it is a *best practice*. After some time I realized that we all should be more careful when using this term and start thinking more critically whenever we hear it.


# My Problem With *Best Practices*
Don't get me wrong, I am not denying the usefulness of anything that was ever called a *best practice*, as there can be situations and environments where there is actually a best way of doing things. A useful framework that can be helpful in recognizing such situations is the [Cynefin Framework](https://www.youtube.com/watch?v=N7oz366X0-8).

![Cynefin Framework](https://upload.wikimedia.org/wikipedia/commons/1/15/Cynefin_as_of_1st_June_2014.png)

For a thorough explanation of it I highly recommend [this article](https://hbr.org/2007/11/a-leaders-framework-for-decision-making), but in short it is a framework that defines different domains (Obvious, Complicated, Complex, Chaotic and Disorder) and helps you assess the kind of situation you are in and what decision making model you should apply.

Situations where there is a relationship between cause and effect, which is easily predictable by anyone and repeatable, fall into the *Obvious Domain*. A good example of such a situation is a recurring issue in your software for which there is already a known maintenance procedure - restarting the software. In this case there is an established best practice.

In other domains there is no obvious relationship between cause and effect. Which might mean that there are multiple different approaches to solving a problem or there is no clear solution yet and there is a need to come up with a new approach. In both of those cases there is no best practice.

In my experience in software engineering we often encounter situations that do not fall in the *Obvious Domain*, we work with complex systems where often [there are no solutions just trade-offs](https://www.goodreads.com/quotes/1411380-there-are-no-solutions-there-are-only-trade-offs). By blindly following *best practices* we might forget about the actual trade-off that we are making as we just assume that it is the *best approach* to take. The better way in my opinion is to critically think about the trade-offs and decide *Which problem do I want to be dealing with in the future?* (I learned that from [Essentialism](https://www.goodreads.com/book/show/18077875-essentialism)).

Even if there are established best practices, our environment does not remain the same, which means that after some time our *best practice* might become outdated. The author of [Think Again](https://www.goodreads.com/book/show/55539565-think-again) even mentions that when there is an established Good/Best practice in the company, people tend to focus on the good parts of the approach while forgetting about the flaws. This leads to an environment, where people are not actively looking for improvements which as a result inhibits learning.

## Summary

Best practices have their place, but we should be careful and only apply them in situations where they do actually make sense. Even where there is a sensible *best practice* in place, we should always look critically at it as it allows us to either find an improvement or apply the approach in a conscious manner.