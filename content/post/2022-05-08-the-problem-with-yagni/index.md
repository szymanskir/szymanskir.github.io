---
title: The Problem With YAGNI
author: ''
date: '2022-05-08'
slug: []
categories: []
tags: []
---


# What is YAGNI about
YAGNI stands for *You aren't gonna need it* and advises that you should only implement things, when you actually need them, and never when you foresee them being needed in the future. The idea is to avoid different kinds of problems that come with a premature implementation:

1. You might build the wrong thing - you wasted time on implementing that
2. You might add unnecessary complexity to your code
3. You used up time that could have been used on something that is actually needed now

However, at the same time we should be careful while using YAGNI as used blindly it might lead us to doing more harm than good.

# My problem with YAGNI
Don't get me wrong, YAGNI is good advice - you want to avoid problems that come with a premature implementation. However, at the same time you should not forget about the expandability of software.

Good examples of where not thinking about future expandability might lead to larger issues are Web APIs or configuration schemas (basically anything that can be considered *client facing*). Let's assume that you define a yaml configuration schema that initially supports defining a single object:

```yaml
field1: <FIELD 1 VALUE>
field2: <FIELD 2 VALUE>
...
fieldN: <FIELD N VALUE>
```

Imagine that during the implementation you start to wonder whether you should support the ability of defining multiple objects of the same type. However, you remain vigilant and remind yourself of the YAGNI principle and proceed with the initial implementation. After some time it turns out that there is a need to support the ability of defining multiple objects of the same type within the configuration like this:

```yaml
section:
- field1: <FIELD 1 VALUE>
  field2: <FIELD 2 VALUE>
  ...
  fieldN: <FIELD N VALUE>
- field1: <FIELD 1 VALUE>
  field2: <FIELD 2 VALUE>
  ...
  fieldN: <FIELD N VALUE>
- field1: <FIELD 1 VALUE>
  field2: <FIELD 2 VALUE>
  ...
  fieldN: <FIELD N VALUE>
```

What just happened here is a **breaking change** and this means that either:
1. All clients need to conform to the new schema
2. You need to continue supporting the previous version

Wouldn't you wish that you started off with a schema that supported the initial use case, but remained flexible in case you needed to support the possibility of defining multiple object:

```yaml
section:
- field1: <FIELD 1 VALUE>
  field2: <FIELD 2 VALUE>
  ...
  fieldN: <FIELD N VALUE>
```

You may think that I am assuming the unlikely scenario of *foreseeing the right thing*. The point I am trying to make here is that we shouldn't use YAGNI blindly and we always should carefully think about the potential risks and consequences of our decision. In the example I described we might face two completely different scenarios:

1. The schema is only used by a couple of internal teams - the cost of migrating those configurations to the new schema is low
2. The scheme is used by millions of users - the cost of migrating those configurations is high

Depending on your environment, thinking about those possible scenarios might result in you making a different decision compared to the one you would make while mindlessly using YAGNI.

# Summary
YAGNI is good advice, but it might do more harm than good in some situations. For example, while designing configuration schemas or Web APIs, we might end up with costly breaking changes as a consequence of blindly applying YAGNI. Therefore, next time you use YAGNI - think about potential risks and consequences that may come from applying it in your situation. 