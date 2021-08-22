---
title: Who the heck is an SDET?
published: false
categories:
  - Testing
---

## Role confusion

Nowadays, A very common title in the Test automation space is that of an **SDET (expanded as
Software Development Engineer in Test)**, Phew! that took me nearly 7 secs to even verbally speak
out :sweat_smile: .

The role was first popularized by major Tech companies like Microsoft and Amazon and now is quite
common to see in job openings. Some companies like Google dropped the `D` in favor of more concise
title abbreviated **SET** (Software Engineer in Test) and naturally many companies followed suit
here as well.

But just who exactly is an SDET?

- What do they do on a team or project?
- What skills should they possess?
- Are they Testers?
- Are they Developers?

Sometimes I hear statements like, "I am a Test automation engineer but would like to move to an SDET
role". Indicating Often, there is a deep confusion on what does it actually mean to be an SDET?

Junior engineers new to the field might inherit this title right off the bat when they first join a
company or mid level engineers might get this when they change jobs, thats certainly one way to
acquire the title, but what is the role all about?

## Skills needed to be an SDET

This post aims to offer some additional perspectives into activities that an SDET performs, skills
that you may consider improving upon or acquiring as an engineer already in this role or aspiring to
become one

I came across one of the best descriptions of the role in the book ** How Google Tests Software by
Whittaker, James A.; Arbon, Jason; Carollo, Jeff. Pearson**

> The Software engineer in test (SET) is also a developer role, except his focus is on testability
> and general test infrastructure. SETs review designs and look closely at code quality and risk.
> They refactor code to make it more testable and write unit testing frameworks and automation. They
> are a partner in the SWE codebase, but are more concerned with increasing quality and test
> coverage than adding new features or increasing performance. SETs also spend close to 100 percent
> of their time writing code, but they do so in service of quality rather than coding features a
> customer might use.

### Closer to a dev role

Let's dissect this statement to arrive at some more concrete conclusions of our own

> SDET is a hybrid role. If we consider a spectrum between a pure developer and a pure tester. An
> SDET is much closer to a developer but still can think like a rock solid tester 🤔

Its also quite obvious that an SDET is a person who would write lots of test code and should be able
to write **clean and well factored code** fluently, Should be able review code whether written by a
fellow SDET or SWE (Software engineer)

An SDET should have a **very good understanding and broad perspective of the System as a whole**
they are responsible for and its application stack in the specific context that they are working on
(Web app, mobile app, Desktop app or a distributed backend system.). So that means not just
understanding how different test automation tools, libraries and frameworks work but how developers
are writing feature code and be able to add coverage to unit, integration, E2E tests in service of
functional or non functional requirements of the system etc.

So it seems like being an SDET is a lot like being a **T-shaped engineer** or a generalist on the
team

So now, we understand the broad expectations from an SDET, you may be thinking are there are some
concrete activities that a person in this role usually performs?

Below are some of the activities that an SDET might typically perform on an Agile Software
engineering team

### Software engineering skills

- Able to write clean, concise, maintainable and extensible code
- Able to review code or design docs written by SWE/Fellow SDET or Test Engineers and provide
  technical feedback
- Writes Automation frameworks that is easy to follow and encourages developers to participate in
  adding test coverage to API, UI, other non functional tests
- Understands good framework development practices and their trade offs and incorporates them in
  Automated test or tool designs
- Able to **author Test automation frameworks from scratch** or significantly improve the status quo
  of existing solutions for their context
- Analyze gaps in Test coverage in unit or integration tests and add more coverage for feature code
- Understands **refactoring techniques** and **design patterns** and knows when to apply them to
  solve problems
- Write **Functional** E2E cases for their application (mobile, web, desktop, API) and Non
  functional cases to provide coverage on performance of an API or apps, Security, Accessibility and
  other aspects
- Able to write mocks, stubs for services to ease development

### CI/CD, Reporting

- Builds **results monitoring and reporting** for the automated tests and uses them efficiently to
  analyse and debug any failures
- Builds general **test infrastructure** and **CI/CD pipelines** across different stacks

### Testing acumen

- Thinks **deeply about the system** and can come up with a Testing and automation strategy to
  mitigate customer risk
- Understands the nuts and bolts of the product and has broad context about the system that he owns
- Increases coverage and steers SWE towards writing more test to address missing gaps
- Participates in writing of **product spec** along with PM/Business functions and is able to advice
  developers on how to build **Testability** into features from inception
- Uses **customer usage pattern** data to validate if the product meets its goals when used by a
  consumer
- Mentors other Junior SDET on the team

## Whats the difference between a Test engineer and SDET?

How is an SDET different from a Test engineer you may ask?

Again the book offers a good summary differentiation

> The test engineer (TE) is related to the SET role, but it has a different focus. It is a role that
> puts testing on behalf of the user first and developers second. Some Google TEs spend a good deal
> of their time writing code in the form of automation scripts and code that drives usage scenarios
> and even mimics the user. They also organize the testing work of SWEs and SETs, interpret test
> results, and drive test execution, particularly in the late stages of a project as the push toward
> release intensifies. TEs are product experts, quality advisers, and analyzers of risk. Many of
> them write a lot of code; many of them write only a little.

The key differentiator here is **user focus**, while there is definitely overlap between an SDET in
terms of automation, the test engineer focusses a lot on **User facing** features, does exploratory
testing and writes automated scripts

## What about tools?

If you notice, I've not called out any specific tools or frameworks in this post and that i've been
purposely vague here.

I have a reason for this. 😉

It's because no two problems in Software engineering are the same. There are different problems of
different sizes that depends on a lot of factors like your company, team, culture, requirements etc
and most of the times the solution is gonna be very heavily context driven

However one thing you can do is to learn multiple testing tools and frameworks so that you form the
intuition to mix and match them to create solutions to testing problems.

> If all you have a hammer, everything looks like a nail.

Thus, master your craft and just like a professional have multiple tools and solutions in your tool
box to be used when the appropriate situation occurs. With time you'll gain lot of experience and
intuition around what could work and what might not.

## What about programming languages?

As an aspiring SDET, You should learn **one programming language deeply first**, it really does not
matter which one you choose but pick one, If you are looking for suggestions go for Java, Python,
JavaScript as they seem to be the most popular ones and being ones in which lot of feature and
automation code gets written

Once you have one language on your tips, go ahead and learn a few others in a more general sense
since as you may have noticed above, you'll have to read lot of feature code and write tests or
tooling in them

With micro services architecture its possible developers in your area might have chosen 2 - 3
different languages and so the ability to read and understand what the code is doing is of paramount
importance

## Realities

This is a full time job, and it would take a lot of time and patience on your part to master your
craft.

In terms of industry realities, you may see some companies don't have this title at all.
