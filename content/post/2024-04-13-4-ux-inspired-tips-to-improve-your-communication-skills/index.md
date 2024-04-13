---
title: 4 UX Design Inspired Tips to Improve your Communication Skills
author: ''
date: '2024-04-13'
slug: []
categories: []
tags: []
---

Communication is an interface for interacting with another person. Just like a UI you use to interact with some digital product.

Similarly to how you have delightful and frustrating apps, you can encounter cases where communication with one person is super fun and easy while in other cases it might be a source of frustration.

In this post I’d like to explore the topic of communication from the perspective of design concepts I learned in [The Design of Everyday Things](https://www.goodreads.com/book/show/840.The_Design_of_Everyday_Things) and how we can leverage UX concepts to make our communication better.
## Tip 1: Provide Visible *System Status* in your Communication Channel
It’s frustrating when you don’t get any information back when communicating with a person.

It’s frustrating because:
1. You might not know when it’s ok to ping again
2. You don’t know when you can realistically expect an answer

Imagine you wrote to a person on Slack that you barely know. You know neither of those two things.

That’s why it’s important to setup statuses on Slack e.g. that you are taking a break or having lunch and that you expect to be back at a given time.

This gives the person additional information on what is happening - like a good error message in the app.

For example, compare

> „An error occurred”

to

> „An unexpected error occurred. Please try to refresh the site. If the error persists pleases tech out on „support@email.com”

This makes the person feel in control of the situation and reduces frustration.

A good heuristic to think about here is: *does the recipient of my message know what will happen next and when will it happen*.

Of course, not all messages require a reply, in those cases it can be a good idea to add a reaction/emoji that shows you read the message (the *message delivered* indicator is not enough).
## Tip 2: Make it Easy to Start the Conversation
A part of the [Human Action Cycle](https://en.wikipedia.org/wiki/Human_action_cycle) is the execution stage where the user plans a series of actions to achieve a specific goal.

Imagine you are new in a project and you have a question - where should you reach out for help?

We should make it easy to know how and where to communicate.

For example:
1. Assign a buddy who is the main point of contact for a new person - that way by default the person can reach out to their buddy
2. Create slack channels with meaningful names and helpful descriptions - this allows a person to quickly find a channel and use it properly (See [Create guidelines for channel names](https://slack.com/help/articles/217626408-Create-guidelines-for-channel-names))
3. If your team maintains an internal service, provide a page for asking for help
  
## Tip 3: Use Forcing Functions in your Messages
Sometimes you might need to communicate with a group of people to get some information from them.

Just sending a question to a group might not be an effective way to do it. For example if you ask a broad and open question, it requires more effort from the recipient to answer them. There is also a risk that you will get answers that do not focus on the thing you are interested in.

That’s why it can be useful to apply lockouts to your communication and provide a list of answers to choose from.

This works very well in case of yes/no questions. For example:

>Hi team, I wanted to propose that we move the review meeting this week from 1:00 CET to 3:00 CET.
> 
>  Our stakeholders are attending a conference and won’t be able to make it. Please react:
>
> 👍Works for me, let’s move it to 3:00pm CET
>
> 👎I don’t like the idea, let’s keep the meeting at 1:00pm CET
>
> 🎈I am fine with both 1:00pm CET and 3:00 CET
>
> 🕐None of the options work for me (please propose a new slot in the 🧵)


Now, not only you made it easier to reply (it's just the matter of picking the right emoji). But you also narrowed down the responses to the ones you are interested in.

## Tip 4: Use Natural Mappings in your Responses

[Natural Mappings](https://www.nngroup.com/articles/natural-mappings/) embed the relationship between the user input and the result of their action.

Imagine you have a more complex discussion about multiple interrelated topics. You provide a response on a similar level of complexity and turns out your colleague is not sure to which parts of your response corresponds to which parts of his original message.

In those cases in can be useful to provide a mapping in form of quoting the parts of the original message you are responding to. For example, let's assume we receive the following message during code review:

*I really like the progress bar you added. It looks really neat!*

*I am not sure I fully understand the way you update the progress in the progress bar - what are the % values based on?*

*BTW there seems to be a test failing in the CI pipeline that is not related to the changes you made here. Have you had a chance to look into it?*

There are 3 different topics within that message, to make our response easy to understand we can quote each part we are replying to, to make the response easier to understand:

> *I really the progress bar you added it looks really neat!*

*Thanks, happy to hear that you like it!*

> *I am not sure I fully understand the way you update the progress in the progress bar - what are the % values based on?*

*I included docs/design/approach_to_calculating_progress.md describing the selected approach along with other considered approaches*. Let me know if that clarifies things!

> *BTW there seems to be a test failing in the CI pipeline that is not related to the changes you made here. Have you had a chance to look into it?*

I created Issue #123 about this. I added the results of my investigation there. Let's continue the conversation there.

## Conclusions
Communication can have a good and bad UX, that means we can leverage UX concepts to make our communication better such as:

1. Providing visible system status
2. Making it easy to start conversations
3. Using forcing functions in messages
4. Using natural mappings in responses
