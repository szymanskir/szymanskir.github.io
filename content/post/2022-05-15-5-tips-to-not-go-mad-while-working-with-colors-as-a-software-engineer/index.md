---
title: 5 Tips To Not Go Mad While Working With Colors As A Software Engineer
author: 'Ryszard Szymański'
date: '2022-05-15'
slug: []
categories: []
tags: []
---

# Why I hated working with colors
I would say that I was always below average in terms of artistic abilities compared to my peers in school. Things were so bad to the point where my mother had to work really hard to help me do my homework for art classes (thanks mom!). I thought that in order to be able to make something *look good or pretty*, you need to be born with some kind of talent.

When I went to university to study Computer Science I thought, that I will never have to worry about such things like design, colors etc. Turns out that Software Engineers build apps that need to *look good*, or if you are a Game Developer you  are diving deep into different areas of [Computer Graphics](https://en.wikipedia.org/wiki/Computer_graphics_(computer_science)) such as animation or rendering.

The nightmares from art classes started coming back again. I would find myself getting frustrated as I had no idea how to make something look good. This year I managed to make some progress and learn some heuristics that allow me to navigate better in the space of UI/UX design. However, there was one particular topic that frustrated me the most - **picking colors**!

Apart from **picking colors** I also hated talking about colors as it would usually lead to endless discussions about someones particular *subjective taste*.

In order to make the subject less frustrating for me, I decided to educate myself on the topic of colors. In this blog post I would like to go through tips that allowed me to navigate better in this space. Those tips are what helped me in becoming slightly less garbage at picking colors and allowed me to find *okayish* colors more quickly.

# Tip 1: Accept that color perception is subjective
My expectation of learning more about colors was that I will finally find a way to pick and discuss colors in an objective manner. However, after reading [Colors Matters. 6 tips on Choosing UI Colors](https://blog.tubikstudio.com/color-matters-6-tips-on-choosing-ui-colors/) I learned that color perception is indeed subjective. There is even a field called [Color psychology](https://en.wikipedia.org/wiki/Color_psychology) that studies how different hues influence human behavior.

Different factors, such as age or your background, influence how you perceive a certain color. For example in Poland one of meanings of the white color is *purity*, while in China white is considered as the color of mourning ([source](https://en.wikipedia.org/wiki/Color_in_Chinese_culture)).

# Tip 2: Use existing color palettes or use established color schemes to generate one
As a Software Engineer, I wouldn't expect from myself to be able to create a great color palette on my own. Thankfully, there are people more knowledgeable on this topic, who have shared their color palettes that we can ~~steal~~ reuse.

An example of that is the [color palette available in Tailwind CSS](https://tailwindcss.com/docs/customizing-colors). Thinking about using yellow? You just got 10 shades of it just like that.

Another thing you can do is leverage established color meanings such as *green* / *red* to convey *positive* / *negative* messages or use warm and cold colors for visualizing warm and cold weather. I learned about that from the [A detailed guide to colors in data vis style guides](https://blog.datawrapper.de/colors-for-data-vis-style-guides/) (highly recommend!).

In case you find yourself in a difficult situation of needing to come up with an initial set of colors on your own, don't worry, the experts got your back. They already did some research on different color schemes that lead to most attractive and effective color arrangements. 

Those color schemes are based on the Color Wheel, which you might have heard about during art classes at school (if you are not familiar with it, check out [Color Theory: Brief Guide For Designers](https://blog.tubikstudio.com/color-theory-brief-guide-for-designers/)). You can think of a color scheme as a heuristic, for example the Monochromatic color scheme works like this:

1. Pick a single color e.g. blue
2. Pick various tones and shades of it

Simple, right? Wrong! How do I pick the right tones and shades? Well, you don't have to! You can use [coloors.co](https://coolors.co) to generate your own palette using a specific color scheme.


# Tip 3: Remember about the medium, accessibility and dark mode
You generated yourself a color palette, however turns out that there are other things to consider:

1. Your colors can be viewed on different devices, which might display colors differently (e.g. an ebook with only black and white colors or *paper* in case your app generates documents that will be printed)
2. How your colors are seen by people with colorblindness
3. Your users might be viewing your colors in dark mode, if your site supports that

In those cases, you can leverage:
1. Color palettes that are already colorblind friendly, printer friendly - you can find some on [colorbrewer2](https://colorbrewer2.org)
2. Use tools that allow you to assess your colors in terms of accessibility such as the [WebAIM contrast checker](https://webaim.org/resources/contrastchecker/) or [VizPallete](https://projects.susielu.com/)

It might be difficult to find a color palette that works in all of the cases, so you might need to use a different color palette for dark mode for example.

# Tip 4: Use the 60-30-10 rule
Picking the colors is one part, the other is applying them in a sensible manner. Here is where the 60-30-10 rule comes in - it states you should use colors in the proportion of 60%-30%-10%. A good way to think about it is clothes: pants are one color (60%), the t-shirt is the other color (30%) and accessories are the third color, e.g. a hat (10%).

According to the [Color Matters. 6 Tips on Choosing UI Colors](https://blog.tubikstudio.com/color-matters-6-tips-on-choosing-ui-colors/) article, such a proportion is thought to be pleasant for human eyes.

# Tip 5: Test if you picked the right colors
You made it this far - you picked a color palette and applied it in a sensible manner. Now is the time to test how the color palette we have chosen is perceived by others. In order to do that you can leverage:

1. [Usability testing](https://en.wikipedia.org/wiki/Usability_testing)
2. [A/B testing](https://en.wikipedia.org/wiki/A/B_testing)

The results of both of those techniques will provide you with input on how you can improve your colors!

# Summary
Picking colors is a difficult task that requires expert knowledge that a Software Engineer might not necessarily have. Don't be discouraged if you feel like it is hard to objectively pick a color, it's because color perception is indeed subjective! 

If you need a color palette, try reusing what is already available or use established color schemes to generate one. However, remember about accessibility, dark mode and that your colors might be seen on different devices.

After you picked the colors, use the 60-30-10 rule and leverage usability testing or A/B testing to make sure that your colors actually work.