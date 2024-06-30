---
title: "2 Reasons Why 'I Can Just Look It Up' Doesn't Work"
author: "Ryszard Szymański"
date: 2024-06-30T10:44:24+02:00
slug: []
categories: []
tags: []
---

In high school I didn’t like subjects like history or biology. I didn’t like the aspect of having to constantly memorize stuff. After all I could *just look that up* when needed, right? I preferred math as I could just internalize how to achieve some things without having to memorize each of the steps to get there. 

During my computer science studies, it turned out that there are still subjects that require some kind of memorization e.g. more complex definitions in mathematics or operating systems concepts (like the file system in Linux or some bash commands).

I would still try to avoid memorization at all costs and focus only on the *understanding* part. However, it limited how well I did in those subjects.

In this blog post I'll describe 2 reasons why just focusing on understanding without memorization was not enough for me.  
## Reason 1: You Focus on Looking Things Up Instead of the Actual Problem

I remember being annoyed at university when I had to write code on paper without access to an editor offering auto-complete. Having an editor would allow me to not have to remember specific syntax.

While memorizing all functions from a library might not be worth it, constantly looking up things like how to define a function/class isn't good either.

Looking up things costs you focus and time. If you are dealing with a complex problem, you want to be dealing with that problem, not on the syntax of your language. By remembering syntax you can stay in the flow and focus your efforts on solving that particular problem.

Just how it’s [faster to read something that is stored in RAM compared to   
reading it from disk](http://static.googleusercontent.com/media/research.google.com/en/us/people/jeff/stanford-295-talk.pdf). Similarly retrieving information that you have memorized can be faster than looking it up.

The more complex the topic you are working on, the more memorizing the basics will support you. 

For example, you might be able to solve a differential equation problem without memorizing the multiplications table and look up each multiplication. But the constant context switching from solving the equation and the multiplication table will hurt your focus.
## Reason 2: Looking up Solutions to Complex Problems is Hard 

I heard *I can just look it up* most often during data structures and algorithms classes at University. Some would complain *why are we learning this stuff if these things are already implemented and provide user friendly APIs*.

This is true to some extent, however what do you do if the already implemented thing does not work as expected? Or how do you know which one to apply to your particular problem?

For example, you learn that *adding an index to a column to a database will speed up queries*. This really isn’t the full picture, as you still need to decide on which type of index you need. 

Let's say you have a slow query that searches through product names based on the user input. Creating [a default B-tree index](https://www.postgresql.org/docs/current/indexes-types.html) might help if you are doing prefix searches (like `col LIKE foo%`), but it won't be used for other searches like `col LIKE %foo%` or `col LIKE %foo`. It might make more sense to use [a GIN index](https://www.postgresql.org/docs/current/textsearch-indexes.html) in this situation.

Unless you are dealing with a problem that someone else has already solved and shared it, you won't be able to look up a solution and you'll need to solve it yourself and this is where a deeper understanding of the basics will pay off.

## Conclusions
Looking things up can be useful. After all you don’t want to necessarily read the source code of Postgres if the same information is provided in a more convenient manner in the documentation.

At the same time, don’t go into the extreme of looking up everything as this will:

1. Prevent you from focusing on the problem at hand as you will first need to solve the problem “that you need to look up” (e.g. syntax)

2. When you hit a complex problem that you can’t look up, you are on your own. By understanding deeply how the thing you are using works, it will make it easier to solve that problem.

That said, memorizing everything also is not a solution. That's why I prioritize memorizing concepts related to the basics that don't change as often e.g. how operating systems works instead of how a new framework works. 
