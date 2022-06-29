---
title: 3 UX Design Concepts That Can Make You A Better Software Engineer
author: 'Ryszard Szymański'
date: '2022-06-16'
slug: []
categories: []
tags: []
---


# Why would software engineers even bother learning UX design skills

Whenever I heard about UI/UX design, I thought I don't need to learn about it because I am not interested in becoming a frontend developer. 

Ironically, in later stages of my career I was getting more involved in frontend development. As a result I am actively learning to improve in that area and this is when I looked into [The Design of Everyday Things](https://www.goodreads.com/book/show/840.The_Design_of_Everyday_Things) book.

After reading the book I have realized that no matter if you are a backend or devops engineer, you probably are developing products with which other humans interact (for example other software engineers) and UX design skills may allow you to build better software (even if it doesn't have an UI!). 

In this blog post I want to describe three UX design concepts that you can use to start creating more user friendly products.

# Concept #1: Importance of feedback
Have you ever gotten frustrated with an unclear error message while programming? You had no idea what is going on and it was driving you crazy?

This is why any tool you are building should provide full, clear information about the results of an action and the current state of the product. For example, if you are building a command line interface, when a user forgets to supply a required argument, instead of providing a vague message like `Error: exception occured.`, try to be specific and helpful to your user `Error: required option '--num_threads' is missing. Run 'tool --help' to see a list of required arguments.`

This is also important when designing APIs. If a client sends a request that doesn't pass validation, you want provide an informative HTTP status code (don't be that person that always returns 200, even when an error occurred) and meaningful error message. The authors of [Best Practices in API Design](https://swagger.io/resources/articles/best-practices-in-api-design/) even emphasize that *Hand holding your end consumer to success whenever they hit a road block working with your API will go a long way in improving developer experience and preventing API misuse.*

# Concept #2: Human slip ups and mistakes
Nobody is perfect and we should accept that humans make mistakes. For example, have you ever made a silly typo in your code that led to hours of debugging? 

When analyzing mistakes we tend to be happy with the explanation of a *human error* and blame it on the users not reading the manual carefully enough. We should design tools in a way that minimizes the chance of our users making a mistake or make it easier for them to recover from the results of an error.

A good example of that is a project initialization library. When you run the command to bootstrap your project and it notices that you are trying to overwrite an existing directory, it will inform you about this and ask you to confirm if this is actually what you want to do.

# Concept #3: Knowledge in the Head and in the World
The author of [The Design of Everyday Things](https://www.goodreads.com/book/show/840.The_Design_of_Everyday_Things) defines two types of knowledge: knowledge in the world and knowledge in the head. To learn how they differ let's go back to the example of a command line interface tool. 

Most of the CLI tools you have interacted with probably offer some kind of a `help` subcommand which allows you to list all available commands. This can be considered as knowledge in the world because you don't have to memorize all available commands - you can always list them. Knowledge in the head are facts that you need to memorize.

The concept can be applied to your pull request checklists - I often encounter an item that states *Update documentation*. This means that all developers need to memorize which documentation they need to update (knowledge in the head). Humans are not perfect, forget things and make mistakes. Therefore it is a better idea to embed that knowledge within the pull request checklist itself. We could write *Update documentation - README, CHANGELOG* and link to respective locations.

# Summary
UX design skills can make you a better software engineer, even if you are not doing frontend related work. For example: 

1. Always provide meaningful feedback such as informative messages when you are throwing an exception
2. Design your tools in a way that minimizes the chances of users making a mistake or make it easier for them to recover from that mistake
3. Save your users from the burden of memorizing things - embed that knowledge in your tools