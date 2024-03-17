---
title: '''More modular code is more maintainable code'' is a lie'
author: ''
date: '2024-03-16'
slug: []
categories: []
tags: []
---

I often hear the following phrase *"thanks to doing ___ the code is now more modular and more maintainable"*. Sounds reasonable, but it doesn't capture the full picture. 

There are cases, when more modularity might make things less maintainable.

First let's establish what I mean by *maintainable*. Maintainable code is code that is easy to change.
## Example 1: Extracting things into a separate package
With that in mind, think about the following situation:
1. You are building an app
2. You implemented a functionality that might be reusable, so you extract it out into a separate package
3. You put that package in a separate repository
4. You get a new app requirement that requires you to change some of the logic that you extracted out of the package and additional changes on the app side as well
5. Now, to implement that requirement you need to make 2 changes in 2 separate repositories
6. You apply the change to the package and release a new version
7. Now you can make a change to the app and bump the version of that package

Now let's imagine we didn't extract a package out of that app. What would happen instead of steps from 5 to 7? 

Well, you would be able to submit a single PR that contains the same changes made in the previous scenario.

We had good intentions, we wanted to make things more modular by keeping things tidy in their own separate packages.

But as a consequence we made it harder to make changes to the app as now our feature implementation requires more steps.

Imagine how difficult things would get, if we had 5 packages in different repos? In the worst case scenario we would need to make 6 changes (5 package repos + 1 app repo) to implement one functionality.

On top of that, we will need to keep track of which package versions are compatible with which app version. This adds on additional complexity.

A keen eye might notice that we could have used a monorepo structure instead. That means keep all packages and the app in a single repository. That would allow us to apply changes in multiple places in a single pull request.

Some technologies provide tooling that makes it easy to keep an app and related packages in a single *container*. For example when using Visual Studio you have [solutions that can contain multiple packages](https://learn.microsoft.com/en-us/visualstudio/ide/solutions-and-projects-in-visual-studio?view=vs-2022).

## Example 2: Keeping styles separate from your components
Another situation, where I faced issues with modularity, is keeping styles separate from components. For example having a dedicated folder for all your stylesheets like this:

```
components/
├─ buttons/
│  ├─ button1.js
├─ form_controls/
│  ├─ form_control1.js

stylesheets/
├─ colors.css
├─ styles1.css
```

This might seem neat at first, but based on the file structure are you able to guess where the styles of `button1` are kept?

Depending on the technology, you might be able to find that information based on the imports and your IDE features might even allow you to get to that file with a single click.

Even if you have that option, the constant jump and forth between the component file and the stylesheets when implementing new changes can cause a large overhead.

Also during code review, you look at a changed css file and need to figure out which components are being affected.

That's why I personally prefer using utility-first CSS (like in [tailwind](https://tailwindcss.com/docs/utility-first)), where I would have no separate files for my styles and just apply a set of class names to my component.

Now, I have both my component code and it's styles in one file making it easier to make edits and review in pull requests.

## Conclusions
Making things more modular does not always make things more maintainable. It can actually make things less maintainable if not used properly.

That's why when modularizing things, let's check if we are not accidentally making things harder to change in the future.

A good heuristic to consider before *extracting things out into a separate module* is ***["the code that changes together, stays together”](https://www.baeldung.com/cs/cohesion-vs-coupling).***