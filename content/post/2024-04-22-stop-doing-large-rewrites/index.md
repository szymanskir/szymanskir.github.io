---
title: Stop Doing Large Rewrites
author: ''
date: '2024-04-22'
slug: []
categories: []
tags: []
---


 You join a project, it’s an existing codebase. As you sit down you notice how messy and suboptimal things are. 

Those things slow you down to the point where you start feeling that *it might be faster if you rewrite the whole thing from scratch instead of trying to implement it alongside the existing code*.

Well, it might not be that easy ;)

In this post I’d like to explore different perspectives of rewriting software, show how risky of a bet that is and whether there are cases where it might indeed make sense.

## Factors to Consider
Before deciding on the rewrite it’s important to consider:

1. Why do we want a rewrite?
2. How large the codebase is and how long did it take to implement it?
3. Was the code written by the same team that will be doing the rewrite?
4. Is the code currently used?
5. How often do we anticipate the codebase to change?

These factors are not mutually exclusive and can impact each other. Let’s look at them one by one.

### Factor 1: Why Do We Want a Rewrite

There might be different reasons for considering a rewrite. I most often hear about a rewrite in the context of refactoring legacy code.

However, there can be other cases, like for example you:
1. hit a limitation of the technology you are using
2. see a benefit of switching to a different technology
3. use a technology that is getting deprecated

This will guide us in learning on what are the anticipated benefits of the rewrite.

In the case refactoring I usually hear *it will make the code more maintainable and easier the change leading to lowered costs*.

When a rewrite is caused by a change of the technology this might be to:
1. improve performance (see [Why Discord is switching from Go to Rust?](https://discord.com/blog/why-discord-is-switching-from-go-to-rust))
2. cut down costs and lower risks e.g. developers of a deprecated technology might be more expensive and less available, a deprecated technology might also mean no security patches


### Factor 2: How Large the Codebase Is

If we want to rewrite the whole codebase we should be aware of how large it is. Or better how long did it take to implement it.

This will tell us at least what magnitudes of effort are we expecting e.g. is it more like months, weeks or years.

That said we shouldn’t treat that as the ultimate estimate, as rewriting estimates might change based on:
1. Who will do the rewrite - is it a team that knows the product well?
2. Does the new technology make things simpler or harder to implement (e.g. are there packages available that might speed up the work)?

### Factor 3: Was the Code Written by the Same Team That Will be Doing the Rewrite

What I often saw in the past is a new team taking over a project requesting time for a ground up rewrite/refactor because how difficult it is to work in the existing codebase.

The codebase would usually have no documentation, it would be so bad to the point to no one knew what is the list of currently used features!

A rewrite in this case is very risky because:
1. We might alter behavior that already exists (which might be a bug that turns out to be a feature used by someone)
2. We might forget about implementing an existing feature 
3. The team doing the rewrite needs to learn the business domain which can lead to additional costs

### Factor 4: Is the Code Currently Used

Doing a rewrite of the whole codebase can be reckless. Chances are that there are multiple features that are rarely used or not used at all.

Let’s say we rewrite those features in Rust and that way improve the performance. How does that impact the business? Did it lower costs? Did it increase the usage of the features? And most importantly - was that benefit worth the cost of the rewrite?

If the code is not used at all, maybe it makes more sense to delete it instead of rewriting it?
### Factor 5: How Often do We Anticipate the Codebase to Change

Another thing to consider is how do we anticipate the codebase to change. 

This might be a stable process that exists in the company for years or is this something that just got created and is more of an experiment/quick prototype.

Let’s say it’s an established process and we do a refactor. Nobody touches that code after the rewrite for multiple years. Was the rewrite worth it?

Well, there is some argument that it might increase morale among the engineers working on that codebase (which is important as it might allow you to retain employees and avoid costs of finding new hires).

But other than that - why touch something that probably won’t change?

## Example Cases
Given the described factors, let's have a look at a couple of potential cases and see if a rewrite is a good idea.

## Case 1: Messy Codebase that is Used a Lot
If the codebase is currently being used, that means there is still a need to maintain it, e.g. react to incidents, fix bugs, provide support for users.

By starting a rewrite we would essentially be doing two jobs:
1. Reimplementing the new system
2. Supporting the old system

Given that new features might start to be requested from users of the old system, you might end in a situation where you are in a big hurry for feature parity. And as a result you end up with two messy codebases instead of one.
## Case 2: Messy Codebase that is Not Used
We do a rewrite of a codebase that is not used. Probably it will remain unused. Unless we address the core issues of the original codebase, e.g. issues causing the users to not want to use the product.

Learn if you are even solving someone's problem, if not, just archive the codebase and move on.

## Case 3: Performance Limitation, Used code
Let's say our codebase is slow and we already tuned everything there is to tune and we are out of ideas.

In the [Discord example of switching from Go to Rust](https://discord.com/blog/why-discord-is-switching-from-go-to-rust) the rewrite to Rust did improve the performance, but we don't know what the ROI of this investment is. I imagine that the team did take into consideration how crucial that service is and how this investment is going to pay dividends over time. Additionally, it is mentioned in the article that it was also meant to improve the user experience, so there was some idea of a business value behind it.

You can [find comments](https://news.ycombinator.com/item?id=22238335) about Go improving it's garbage collector and people questioning the rewrite. We don't know if the improvements of Go's garbage collector would have been enough.

Which further shows how difficult those decisions are, e.g. what would you pick: a rewrite or fixing edge cases in a garbage collector?

## Alternatives to Large Rewrites
 Large rewrites are risky bets, they can get really expensive and the benefits can be difficult to quantify.

That’s why to manage risks of bad time investments it’s better to work in small steps. For example continue developing new features in your legacy codebase, but try to add in some minor improvements ([The key points of Working Effectively with Legacy Code](https://understandlegacycode.com/blog/key-points-of-working-effectively-with-legacy-code/) describes useful techniques)

Over time this will improve the codebase and will do it in places that are changed most often. This works well if we are not changing a fundamental technology in our codebase.

In case of rewrites into another technology, you could rewrite only some very specific part as a start. For example if you have a bottleneck in the R code, rewrite this part into C++ and call it from R. That way, you make the change smaller and less risky.

If that’s not a possibility and you can’t link technologies together, do a quick prototype, estimate the potential ROI and make a decision based on that.
## Conclusions
Large software rewrites are risky and difficult.

Before suggesting or attempting one, think about
1. Why do you want to do a rewrite?
2. How big the codebase is?
3. Is the rewrite done by the original authors?
4. Is the code currently used?
5. How often do we anticipate the codebase to change?

Even better, put that all in a doc and quickly estimate a potential ROI. Prepare initial small steps, after each step reassess if it’s worth to continue the rewrite.

I am not saying to never do rewrites, but before I would do one I would consider all the less risky and costly options.