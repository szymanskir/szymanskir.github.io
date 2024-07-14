---
title: Quick Calls Are Not That Quick
author: ''
date: '2024-07-14'
slug: []
categories: []
tags: []
---
## Introduction
Imagine that you are being reached out to by multiple people asking different questions. You know the answers to all of the questions and you feel like typing is slowing you down. Therefore, you ask them to have quick calls to speed things up.

But is it actually speeding things up? In this blog post I'd like to look into the time costs of exchanging information and check if *Quick Calls* are actually worth it.

## The Premise Of Being More Productive
It is true that we speak faster than we write. [According to the National Center for Voice and Speech](https://virtualspeech.com/blog/average-speaking-rate-words-per-minute), the average speaking conversation rate is about **150 words per minute**.

At the same time the [American Society of Administrative Professionals](https://www.asaporg.com/efficiency-skills/average-words-per-minute-typing-how-fast-is-fast-enough) reports that the average typing speed is around **40 words per minute**.

This means that by speaking I become almost 4x faster, right?

Actually, this is only one dimension of the whole issue. After all, there are also other factors that influence the time costs:
1. how long it takes for recipients to read/hear the message;
2. context switching costs of the recipients.

In the next section, let's try to estimate the time costs of synchronous calls compared to asynchronous information exchange.
## Time Cost Analysis
Before we begin our simulations let's establish a couple of assumptions:
1. Speaking Speed: **150 words per minute** ([source](https://virtualspeech.com/blog/average-speaking-rate-words-per-minute))
2. Writing Speed: **40 words per minute** ([source](https://www.sciencedirect.com/science/article/abs/pii/S0749596X19300786))
3. Reading Speed: **238 words per minute** ([source](https://www.sciencedirect.com/science/article/abs/pii/S0749596X19300786)) 
4. Context Switching Costs:  **23 minutes** ([source](https://www.loom.com/blog/cost-of-context-switching))

A synchronous call includes the following time costs:
1. Time to *say the message* (`words_count / 150`)
2. Time to listen to the message (equal to the time to say the message for each recipient: `(words_count / 150) x recipients_count`)
3. Time of Context Switching (`23 x recipients_count`)

We can summarize the cost for synchronous calls as:
```
sync_time_cost = (words_count / 150) + recipients_count x (words_count / 150 + 23)
```

> **Note:** We assume no context switching time for the *speaker*

For asynchronous calls we need to include:
1. Time to *write the message* `words_count / 40`
2. Time the read the message by recipients `(words_count / 238) x recipients_count)`

> **Note:** We assume that the message is read by recipients during their dedicated message checking slots, so there is no context switching cost. If you work in an environment where you constantly get messaged and need to respond quickly, then you might also need to include costs of context switching.

We can summarize the cost for asynchronous message exchange as:
```
async_time_cost = (words_counts / 40) + recipients_count x (words_count / 238)
```


As we can see, there are 2 variables in those equations:
1. `words_count` - how long our message is
2. `recipients_count` - how many people need to read/hear our message

Let's perform 2 simulations to see how those values impact the time costs.

### Simulation 1: Time Cost Change Based On Number Of Recipients
Let's assume that our call would indeed be quick and take only 10 minutes. That means our message is composed of 1500 words.

Let's see how the time cost changes from 1 to 6 recipients:

| Words Count             | 1500     | 1500     | 1500     | 1500     | 1500     | 1500     |
| ----------------------- | -------- | -------- | -------- | -------- | -------- | -------- |
| Recipients              | 1        | 2        | 3        | 4        | 5        | 6        |
| Sync Cost               | 43       | 76       | 109      | 142      | 175      | 208      |
| Async Cost              | 44       | 50       | 56       | 63       | 69       | 75       |
| **Sync to Async Ratio** | **0.98** | **1.52** | **1.95** | **2.25** | **2.54** | **2.77** |

Turns out the sync call is faster when we only have 1 recipient. For more recipients the async cost is smaller. For example for a team of 3, synchronous information exchange is almost twice as costly (time wise) compared to doing it async.

### Simulation 2: Time Cost Change Based On Message Length
Let's assume that we work in a team of 5. Let's see how the time cost changes with higher word counts.

| Words Count             | 750      | 2250     | 3750     | 5250     | 6750     | 8250     |
| ----------------------- | -------- | -------- | -------- | -------- | -------- | -------- |
| Recipients              | 5        | 5        | 5        | 5        | 5        | 5        |
| Sync Cost               | 145      | 205      | 265      | 325      | 385      | 445      |
| Async Cost              | 35       | 104      | 173      | 242      | 311      | 380      |
| **Sync to Async Ratio** | **4.14** | **1.97** | **1.53** | **1.34** | **1.24** | **1.17** |

It seems that the longer our message, the more we start to benefit from the higher speaking speeds. However, even for a message as long as 8250 words (which corresponds to a 55 minute speech BTW) async is still less costly (time wise).

## Long Term Costs
Our simulations only look at the short term - the cost of just delivering the message. However, our information exchange strategy can also impact some long term costs.

For example, if we go with async and we exchange information through public channels on Slack:
1. Those messages are searchable in Slack search increasing their reach
2. Written out message can be turned into documentation
3. You can copy and paste the same message or link to a message if you get a similar question

Similarly for synchronous messaging, we can create recordings and with automated transcripts we can also make them searchable.

> **Note:** If you forget to record, the information becomes tribal knowledge stored in the heads of meeting participants (or forgotten with time).

Depending on the available tooling you might prefer one or the other. Although, written out messages are easier to update than recordings ;)

## Conclusions
Speaking is faster than writing, but it doesn't take into account the time costs of recipients which includes hearing out the message and switching context.

Synchronous calls may be the less time consuming option if we don't have many recipients and our message is long enough to benefit from *speaking* speeds.

After playing around with the model for my situation all cases showed that async is less costly (time wise) for information exchange. That's why if I don't need immediate interactions with other team members, async will be my way to go. In addition, I get the potential long term benefits of writing out the message.

I encourage you to use the model and see what makes more sense in your case (and add additional variables if needed!).

Of course there are benefits to synchronous meetings such as:
1. building rapport
2. being able to take immediate action
3. avoiding wait times of async communication

But let's not lie to ourselves that we are doing quick calls to be more productive (time wise).

