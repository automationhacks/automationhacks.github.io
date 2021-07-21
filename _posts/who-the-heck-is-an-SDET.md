---
title: Who the heck is an SDET?
published: false
categories:
  - Testing
---

A very common title in the Software Testing space is that of a SDET (expanded as **Software
Development Engineer in Test**) popularized by major Tech companies like Microsoft and Amazon.

Some companies like Google dropped the `D` in favor of more concise title **SET** (Software engineer
in Test) and naturally many companies followed suit.

But just what or who exactly is an SDET?

- What skills should they possess?
- Are they Testers, QA?
- Are they Developers?
- Are they Test automation engineers?

Whats the difference between these?

Junior engineers new to the field might inherit this title when they first join a company or mid
level engineers might get this when they change jobs, thats certainly one way to acquire the title,
but what is the role all about?

Often, there is a deep confusion on what does it actually mean to be an SDET?

I hear statements like, I am a Test automation engineer but would like to move to an SDET.

This post aims to offer some additional perspectives into activities, skills that you may consider
improving upon as an engineer in this role or aspiring to become one

I came across one of the best descriptions of the role in the book ** How Google Tests Software by
Whittaker, James A.; Arbon, Jason; Carollo, Jeff. Pearson**

> The Software engineer in test (SET) is also a developer role, except his focus is on testability
> and general test infrastructure. SETs review designs and look closely at code quality and risk.
> They refactor code to make it more testable and write unit testing frameworks and automation. They
> are a partner in the SWE codebase, but are more concerned with increasing quality and test
> coverage than adding new features or increasing performance. SETs also spend close to 100 percent
> of their time writing code, but they do so in service of quality rather than coding features a
> customer might use.

Let's dissect this statement to arrive at some more concrete conclusions of our own

Its quite obvious that an SDET is a person who should be able to write **clean and well organized
code** fluently, Should be able review code whether written by a fellow SDET or SWE (Software
engineer) and possesses sound Technical acumen

What does it mean to have good Technical acumen you may ask?

Let's just say that an SDET should have a very good understanding and broad perspective of the
System they are responsible for and its stack and the specific context that they are working on (Web
app, mobile app, Desktop app or a distributed backend system.). Being a generalist in multiple of
these streams is usually a plus.

Below are some activities that an SDET might typically perform on an Agile Software engineering team

- Able to write clean, concise, maintainable and extensible code
- Able to review code written by SWE or SDET's or QA's
- Analyze gaps in Test coverage in unit or integration tests and add more coverage for feature code
- Understands **refactoring techniques** and **design patterns** and knows when to apply them to
  solve test automation problems
- Understands good framework development practices and incorporates them in Automated test design
- Able to **author Test automation frameworks from scratch** for their context, E2E Functional on
  mobile, web, desktop, API or Non functional like Load, stress on API or apps, Security,
  Accessibility etc
- Builds **results monitoring and reporting** for the automation framework and uses them efficiently
  to analyse and debug any failures
- Writes framework that is easy to follow and encourages developers to participate in adding test
  coverage
- Able to write mocks, stubs for services
- Thinks deeply about the system and can come up with a Testing and automation strategy
- Understands the nuts and bolts of the product and has broad context about the system that he owns
- Participates in writing of product spec along with business person and is able to advice on how to
  build Testing and quality into features that would be beneficial for the end customer
- Uses customer usage pattern data to validate if the product meets its goals when used by a
  consumer
- Mentors other Junior SDET on the team

How is an SDET different from a QA?

Again the book offers a good summary differentiation

> The test engineer (TE) is related to the SET role, but it has a different focus. It is a role that
> puts testing on behalf of the user first and developers second. Some Google TEs spend a good deal
> of their time writing code in the form of automation scripts and code that drives usage scenarios
> and even mimics the user. They also organize the testing work of SWEs and SETs, interpret test
> results, and drive test execution, particularly in the late stages of a project as the push toward
> release intensifies. TEs are product experts, quality advisers, and analyzers of risk. Many of
> them write a lot of code; many of them write only a little.
