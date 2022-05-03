---
title: 3 Strategies for Testing Database Interactions for Software Engineers
author: ''
date: '2022-05-02'
slug: []
categories: []
tags: []
---

# Why is it Important to test Database Interactions
Chances are you are writing software that interacts with some kind of a database. This might be a dashboard that fetches data from a database and visualizes it in a convenient manner or a classic [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) application that uses a database for persistent storage.

Those interactions can be a key element of your app that need to be working at all times. Imagine your dashboard not showing any visualization because there is a bug causing an error while fetching the data from the database, or even worse it is fetching the data incorrectly resulting in incorrect insights which then leads to incorrect decisions being made.

Database interactions can get quite complex and manual testing can be both slow and error prone. That is why it is important to have a suite of automated tests that will keep you certain that your database interactions are working at all times and give you a fast feedback loop to allow you to develop new functionalities faster.

In this post I want to go through testing strategies I have learned about and found useful in my journey as a software engineer.

# Strategy 1: Use Test Doubles
Code that interacts with databases can usually be divided into two categories:
1. The code that actually performs the database interaction (e.g. a function that sends an SQL query and retrieves the result)
2. The code that does something with the results retrieved from a database

An example of such code could be a function that:

1. Fetches data on the air quality per region from the database (code that performs the actual database interaction)
2. Visualizes this data in form of a map (code that uses results retrieved from the database)

Using test doubles focuses on testing the code that falls into the 2nd category. In those cases we do not need an actual instance of the database, we just need example results that can be used for testing our visualization. In this case, we might avoid hitting the actual database by using a test double, for example a stub that contains a canned answer. In our case example database results.

This will lead to our test running the following code

1. "Pretend to run a database interaction" and return a preconfigured result
2. Run the code that processes those results
3. Assert the result of the processing from step no. 2

When it comes to the tools that you can use for those types of tests - any mocking framework will do, like for example:
1. [Mocking functionalities in Spock](https://spockframework.org/spock/docs/1.0/interaction_based_testing.html) (Java)
2. [Moq](https://github.com/moq) (C#)
3. [mockery](https://github.com/r-lib/mockery) (R)

# Strategy 2: Use a Simpler Database
Our previous strategy allowed us to test code that makes use of the results of database interactions. What about the code that actually performs the interaction? With time our SQL queries can start containing quite complex logic, which also needs to be tested. That situation can be often encountered when we want to perform our calculations on the database instead of doing them inside of our application in order to improve performance. 

In those cases it might be helpful to use simpler types of database that can be created in memory or in form of a file. As a result we do not need to run a separate database server, which makes our tests simpler and faster to run. Good examples of *simpler databases* are [SQLite](https://www.sqlite.org/index.html) (see example usage in [C#](https://docs.microsoft.com/en-us/ef/core/testing/testing-without-the-database#sqlite-in-memory) or [R](https://withr.r-lib.org/reference/with_db_connection.html)) or H2 ([see usage in Spring](https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html#testcontext-ctx-management-env-profiles)).

Your test could then be composed of the following elements:

1. Setting up an in memory database with test data
2. Running the code that performs the database interaction
3. Asserting if the retrieved result corresponds to what you expected

# Strategy 3: Use an Actual Database 
Simpler databases have their limitations and might not allow us to test fully our database interactions. For example queries that make use of database specific functions such as `ILIKE` or `hstore` in Postgres. In those cases we need an actual instance of the database.

Running an actual database instance can get quite complex - having to install additional software and configure everything, not to mention all remaining challenges that come with automating the setup of database instances and their clean up during our tests. Thankfully, there is a simpler way, you can use a tool like the [testcontainers](https://www.testcontainers.org/) library - it allows you to create throwaway instances of databases in form of [Docker](https://www.docker.com/) containers that can be used in your tests. There are ports of [testcontainers](https://www.testcontainers.org/) available for [Go](https://github.com/testcontainers/testcontainers-go), [C#](https://github.com/testcontainers/testcontainers-dotnet), [node](https://github.com/testcontainers/testcontainers-node), [scala](https://github.com/testcontainers/testcontainers-scala), [Python](https://github.com/testcontainers/testcontainers-python). If you are looking for a similar tool in R, you can check out my prototype called [magician](https://github.com/szymanskir/magician).

Those types of tests can give you the highest level of confidence that your code will be working on your production database. However, at the same time those tests are the most complex and can be quite slow compared to tests that use the two previous strategies.

# Summary
Database interactions are key elements of applications and a potential issue in that area can drastically lower the usefulness of your app. Therefore, it is important to cover those interactions with tests, to make sure that with each introduced change, things are working as expected. 

Database interactions can be tested using 3 strategies:
1. Using Test Doubles
2. Using Simpler Databases (e.g. [SQLite](https://sqlite.org/index.html))
3. Using Actual Databases through a tool like [testcontainers](https://www.testcontainers.org/)

The three strategies are mentioned in order of increasing test complexity (and test times) and levels of confidence those tests can give us. Therefore make sure that you use them in a proportion that makes the most sense in your project (e.g. following the [test pyramid](https://alisterbscott.com/kb/testing-pyramids/) principle).