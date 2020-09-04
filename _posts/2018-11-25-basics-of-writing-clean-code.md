---
id: 47
title: 'Basics of writing Clean code:'
date: 2018-11-25T14:44:56+00:00
author: Gaurav
layout: post
permalink: /2018/11/25/basics-of-writing-clean-code/
publicize_twitter_user:
  - __gaurav_singh
publicize_linkedin_url:
  - null
categories:
  - Programming
---

![A python flask program](https://cdn-images-1.medium.com/max/800/0*bPi6O9LvzPGB8CGo)

A python flask program

I recently read my first iteration of <a href="https://www.amazon.in/dp/B001GSTOAM/ref=dp-kindle-redirect?_encoding=UTF8&btkr=1" target="_blank">Clean Code</a>, the famous book by the prolific Uncle bob martin and it was one of the most delightful and eye opening experiences of my life as a programmer. There were lots of amazing takeaways from that book and personally would _highly recommend_ it to folks who want to improve their craft in coding.

### Why this&nbsp;post?

> Master programmers think of systems as stories to be told rather than programs to be written. — Robert C Martin.

Though it is not possible to summarize the entire book’s learnings in a blog post, i wanted to list down some practices/learnings from the book that IMHO can improve the quality of the code that we write each and every day.

This blog is not an attempt to explain each and everyone of them _(For that, you as a reader can just pick up the awesome clean code book 😉 or google)_ but more as a suitable way for you to **_“Know! what you Don’t know, you don’t know”_**

Well let’s get started, Shall we?

### Universal principles to follow:&nbsp;🌏

There are some principles which are **so** universal in nature and are found repeated in so many different blogs and articles that they deserve a special mention.

  * Avoid duplication anywhere in code(Famously known as **DRY** principle — Don’t repeat yourself )
  * Follow <a href="https://dzone.com/articles/the-solid-principles-in-real-life" target="_blank"><strong>SOLID</strong></a> principles to write clean classes and well organized API’s
  * Follow <a href="https://sourcemaking.com/design_patterns" target="_blank">design patterns</a> and its associated terms **if it fits the problem space that you are trying to solve**. This instantly makes **_your_** __code much more accessible to fellow programmers
  * Follow <a href="https://dzone.com/articles/the-genius-of-the-law-of-demeter" target="_blank">law of demeter</a> to enable less coupling and more cohesion

> Law of Demeter says that a method f of a class C should only call the methods of these:

> • C

> • An object created by f

> • An object passed as an argument to f

> • An object held in an instance variable of C

  * Follow **three laws of TDD**, and keep your **test code** as clean (or even more so) as production code.

> **First Law:** You may not write production code until you have written a failing unit test.

> **Second Law:** You may not write more of a unit test than is sufficient to fail, and not compiling is failing.

> **Third Law:** You may not write more production code than is sufficient to pass the currently failing test.

### Functions

> A Function should do one thing only and do it **really** well

Certain tips for writing effective functions:

  * Avoid passing boolean into a function, this is a hint that func has an `if` statement within which causes it to do more than one thing.
  * Functions should either do something or answer something, but not both. This ensures a function does not have hidden side effects. e.g a func named `isPresent()` should only return a bool and not do any other operations
  * **Prefer** Exceptions to Returning Error Codes and extract error handling `try catch` into their own function.
  * Avoid output arguments. Function if it has to, should change state of its owning object
  * Code should always be separated with blank line to club logical blocks together. Think of different lines of code as **thoughts** and then always think of organizing similar thoughts together
  * Each function should read like a newspaper, every functions implementation following its call and **having less vertical density**
  * Don’t return null

### Object and data structures:

  * Variables should be **private** so that we can change their type or implementation when required. There is no need to add getters/setter to each variable to expose them as public.
  * Hiding implementation is **not just a matter of putting a layer of functions between the variables**. Hiding implementation is about **abstractions**! We do not want to expose details of data but rather express data as **abstract terms**

### **Exception handling:**

  * Try and extract `try catch` blocks into separate well named functions. Having them mixed with other code just confuses the structure of the program. This is inline with “Function should do one thing”, Well error handling is one thing. 😅
  * Prefer returning Exceptions instead of Error Codes.
  * Each exception that you throw should provide enough context to determine the source and location of an error.

### Variables:

  * Variables should be declared as close to their usage as possible.
  * Keep variables private and only expose **necessary** interactions as well defined **abstractions.** Avoid senseless getters and setters which expose all variables unnecessarily

### Comments

> The only truly good comment is the comment you found a way **not to write**.

  * Don’t Use a Comment When You Can Use a **well named** Function or a Variable
  * Any comment which forces you to look into another module for meaning has failed miserably in communicating and is not worth it at all.
  * _Don’t comment bad code, Rewrite it. — _Brian W. Kernighan and P. J. Plaugher

### Boundaries

  * Always wrap third party code/API to minimize your dependency on it and allow the freedom to move to a different one in future without changing the consuming code.

### Code organization and&nbsp;Design:

  * Nearly all code is read left to right and top to bottom. Each line represents an expression or a clause, and each group of lines represents a **complete thought**. Those thoughts should be **separated from each other with blank lines**
  * Local variables should be declared as close to their usage as possible.
  * Instance variables should be declared at top of the class since in a well defined class they would be used by multiple functions
  * If one function calls another, they should be vertically close, and the **caller should be above the callee**, if at all possible. This gives the program a natural flow.
  * Try to follow the **“The Principle of Least Surprise”** any function or class **should implement the behaviors** that another programmer could reasonably expect.
  * It is **NOT** necessary to do a **Big Design Up Front(BDUF)**. In fact, BDUF is even harmful because it inhibits adapting to change, due to the **_psychological resistance to discarding prior effort_** and because of the way architecture choices influence subsequent thinking about the design.

> According to Kent Beck, a design is “simple” if it follows these rules (In order of importance:

> • Runs all the tests

> • Contains no duplication

> • Expresses the intent of the programmer

> • Minimizes the number of classes and methods

### Tests

Clean tests should follow F.I.R.S.T principles:

  * **Fast: ⏩** Tests should be fast. They should run quickly. When tests run slow, you won’t want to run them frequently
  * **Independent: 🆓** Tests should not depend on each other. One test should not set up the conditions for the next test. You should be able to run each test independently and run the tests in any order you like.
  * **Repeatable: 🔁** Tests should be repeatable in any environment. You should be able to run the tests in the production environment, in the QA environment, and on your laptop while riding home on the train without a network.
  * **Self-Validating: ✅** The tests should have a boolean output. Either they pass or fail. You should not have to read through a log file to tell whether the tests pass.
  * **Timely:** ⏲The tests need to be written in a timely fashion.

Apart from this:

  * Ensure you write tests **just for a single concept**. Doing too many things in a test is usually a sign that it needs to be broken down.

Well that’s it folks!

Honestly i think it is going to take loads of practice and few more iterations through this and many other books to drill these principles into my subconscious. But heck!, it’s going to be a fun journey.

If you found this blog interesting. Why not share with a friend or colleague? I am happy to hear if you any thoughts or feedback on this.

Till next time, Happy learning and coding. Cheers! 😁