---
title: 3 Issues Of Dividing Tasks By Components
author: ''
date: '2024-07-06'
slug: []
categories: []
tags: []
---

Imagine you are working on a new feature of your app. It involves changes in the data model, the backend service and the UI.

You might be tempted to divide this work into tasks based on the components of the system:
1. Task for implementing the UI
2. Task for implementing the backend endpoint
3. Task for adjusting the data model

While this seems reasonable at first, there are problems with this approach.

In this blog post I’ll describe those issues along with an alternative way to break down work. 

## Issue 1: Not Building With The End In Mind
Let’s go back to our example. You begin your work on the backend endpoint. All of your thinking is now enclosed by the boundaries of your backend service.

You spend a week on handling all potential edge cases and discussing them with the business team. 

After a week someone picks up the UI related task. They look at the responses from the backend service and they notice that they don’t have everything they need to display the required UI. 

In addition, the response is returned in such a form that is not convenient to use on the frontend side.

It’s even worse as the required information never made it to the original data model or endpoint. Those tasks were so focused on the backend/database side that no one noticed this important control in the UI.

This is a classic case of unknown unknowns appearing (which appear only at the point when you actually try to implement the solution).

## Issue 2: Building Towards The Middle
The way we break down tasks might encourage the team to start building from opposing ends to meet in the middle. For example:
* 1 Developer works on the backend and the data model
* 1 Developer works on the UI

They think that they are speeding things up by parallelizing work. Or they are forced to do it by the business to show that they are doing everything they can to meet a deadline.

Let’s assume that both of the developers are finished with their work and it’s time for the grand finale to connect the frontend to the backend. You are ready to make that API call from the frontend to the backend and it turns out that they don't work together and major adjustments are needed to make them compatible.

Now, you need to tell your stakeholders that the work that was almost done requires a major refactor of the existing solutions to make them work together (or you need to apply a hacky workaround).


![Misaligned Brigde Meme](/misaligned_bridge.jpg)

## Issue 3: Delayed Shipping of Value
Dividing tasks in the mentioned way leads to tasks that don’t provide business value when finished.

After all, if you have the database and API endpoints ready, but all users need a UI to interact with them - you are not delivering value as no one is using what you created (yet!)

Worst part? If you work that way it might take weeks/months of work before you get to the UI and have something shippable.
## Alternative Approach

Instead of dividing work by component, divide it into independent business cases. 

Let’s use a calculator app as an example. You can start off with supporting addition, then move on to multiplication and later on worry about things like square roots or cosines.

Each task to be completed requires the functionality to be ready to use by end users. The fact that you need to make backend and database changes are implementation details.

Thanks to this approach:
1. You are enclosed within the business need
2. Your goal is to have a shippable feature
3. You reduced the number of dependencies within tasks as the business need is independent of others

## Conclusions

Dividing tasks by software components leads to:
1. Building without having the end in mind
2. Building towards the middle leading to misalignment
3. Delayed value shipping

Instead, divide the work into business cases and make it your goal for each task to deliver business value.


