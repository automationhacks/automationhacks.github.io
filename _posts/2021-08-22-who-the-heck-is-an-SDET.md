---
title: Who the heck is an SDET? 😕
excerpt:
  "Software development engineer in Test is a popular role/title in Testing space. In this post I
  share my thoughts on what this role means and some of the skills needed to succeed in this"
permalink: /2021/08/22/who-the-heck-is-an-SDET
categories:
  - Testing
  - "Test automation"
tags:
  - "Testing"
  - "Advice"
---

Nowadays, A very common title in the Test automation space is that of an **SDET (expanded as
Software Development Engineer in Test)**, Phew! that took me nearly 7 secs to even verbally speak
out the full form. 😅.

Jokes apart, The role was first popularized by major Tech companies like Microsoft and Amazon and
now is quite common to see in job openings across the world. Some companies like Google dropped the
`D` in favor of more concise title abbreviated **SET** (Software Engineer in Test) and naturally
many companies followed suit here as well.

But just who exactly is an SDET?

- What do they do on a team or project?
- What skills should they possess?
- Are they Testers?
- Are they Developers?

Sometimes I hear statements like, "I am a Test automation engineer but would like to move to an SDET
role". Indicating often, that there is a deep confusion on what does it actually mean to be an SDET?

Junior engineers new to the field might inherit this title right off the bat when they first join a
company or mid level engineers might get this when they change jobs, thats certainly one way to
acquire the title, but what is the role all about?

## Skills needed to be an SDET 👨‍💻

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

### Closer to a dev role ⚔️

Let's dissect this statement to arrive at some more concrete conclusions of our own

> SDET primarily is a hybrid role. If we consider a broad spectrum between a pure developer and a
> pure tester. An SDET is much closer to a developer but still someone who can think like a rock
> solid tester 🤔

Its also quite obvious that an SDET is a person who would write lots of test code and should be able
to write **clean and well factored code** fluently, Should be able review code whether written by a
fellow SDET or SWE (Software engineer)

An SDET should have a **very good understanding and broad perspective of the System as a whole**
they are responsible for and its application stack in the specific context that they are working on
(Web app, mobile app, Desktop app or a distributed backend system).

So that means not just understanding how different test automation tools, libraries and frameworks
work but how developers are writing feature code and be able to add coverage to unit, integration,
E2E tests in service of functional or non functional requirements of the system etc.

We can envision an SDET being a lot like being a **T-shaped engineer** or a generalist on the team
who obsesses about quality

So now, we understand the broad expectations from an SDET, you may be thinking are there are some
concrete activities that a person in this role usually performs on an Agile Software engineering
team?

Below are some of them:

### Software engineering skills

- Able to write clean, concise, maintainable and extensible code
- Able to review code or design docs written by SWE/Fellow SDET or Test Engineers and provide
  technical feedback
- Write Automation frameworks that are easy to follow and encourages developers to participate in
  adding test coverage at appropriate level
- Understands good framework development practices and their trade offs and incorporates them in
  Automated test or tool designs
- Able to **author Test automation frameworks from scratch if needed** or significantly improve
  existing solutions
- Analyze gaps in Test coverage in unit or integration tests and add more coverage for feature code
- Understands **refactoring techniques** and **design patterns** and knows when to apply them to
  solve problems
- Write **Functional** E2E cases for their application (mobile, web, desktop, API) and Non
  functional cases to provide coverage on performance of an API or apps, Security, Accessibility and
  other quality concerns
- Able to write mocks, stubs for services and build tooling to ease development workflows

### CI/CD, Reporting

- Builds **results monitoring and reporting** for the automated tests and uses them efficiently to
  analyse and debug any failures
- Builds general **test infrastructure** and **CI/CD pipelines** across different stacks

### Testing acumen

- Thinks **deeply about the system** and can come up with a Testing and automation strategy to
  mitigate customer risk
- Understands the **nuts and bolts of the product** and has broad context about the system that they
  own
- Increases coverage and steers SWE towards writing more test to address missing gaps
- Participates in writing of **product spec** along with PM/Business functions and is able to advice
  developers on how to build **Testability** into features from inception
- Uses **customer usage pattern** data to validate if the product meets its goals when used by a
  consumer
- Mentors other engineers on the team

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

The key differentiator here is **user focus**, while there are definitely overlaps between an SDET
in terms of automation, the test engineer focusses a lot on **User facing** features, does
exploratory testing and writes automated scripts

## Some common questions and realities

I have been doing this for sometime and in my experience. This role is a full time job, and it takes
time, patience and lot of experiments to really master the craft. I've called some additional on the
ground realities below:

### What about tools? 🧰

If you notice, So far, I've **not** called out any specific tools or frameworks in this post and
that i've been purposely vague here. I have a reason for this. 😉

It's because no two problems in Software engineering are the same. There are different problems of
different sizes and most of the times the solution is gonna be very heavily context driven depending
on a lot of factors like your company, team, culture, requirements etc

A solution that works in a small startup might not work for an organization where 200+ engineers
work on similar code. Thus with each level of scale your approaches might differ.

However, one thing you _must_ do is to learn multiple testing tools and frameworks either on the job
or in your nights and weekends so that you form the intuition and have a wide enough experience to
mix and match them to create solutions to testing problems.

You may have already come across below quote:

> If all you have a hammer 🔨, everything looks like a nail.

Thus, **master your craft** and just like a professional have multiple tools and solutions in your
tool belt 🧰 to be used when the appropriate situation occurs. With time you'll gain lot of
experience and intuition around what could work and what might not.

### What about programming languages? 👨‍💻

As an SDET, You should learn **one programming language deeply first**, it really does not matter
which one you choose but pick one and stick with it for sometime, If you are looking for suggestions
go for Java, Python or JavaScript as they seem to be the most popular ones and also a lot of feature
and automation code gets written in these.

Once you have one language on your tips, **go ahead and learn a few others** in a more general sense
since as you may have noticed above, you'll have to read lot of feature code and write tests or
tooling in them

With micro services architecture its possible developers in your area might have chosen 2 - 3
different languages and so the ability to read and understand what the code is doing is of paramount
importance

### What if there is no SDET role at the company?

Many companies might not have an SDET title at the company. They may have common titles like Quality
engineer, QA Engineer, QA Automation engineer, Test engineer, Test automation engineer, so on and so
forth.

And let me tell you a secret. 😉 ㊙️

> Titles don't matter

What matters is that these activities should happen as they bring lot of value to a Software
engineering team and product and you as a SDET should do take it upon yourself to evangelize these
in your team and company regardless of the title that you possess. Don't seek permissions, go ahead
and improve the status quo.

I had previously written couple of posts on these topics around titles and how much confusion they
add if not being setup properly in a company, feel free to read them:

- [Testers identity crisis - QA/QE/AE/SDET/SET/TA? 🤷]({% link
  \_posts/2020-10-08-testers-identity-crisis-qa-sdet-te-dev.md% })
- [The problem with titles for
  testers]({% link _posts/2020-02-29-the-problem-with-titles-for-testers.md %})

### Lone SDET on the team?

Another common question is, what if i'm the lone SDET on a team?

Well firstly buckle up since its not gonna be an easy ride, and secondly **cheer up** since now you
have some constraints at hand and can figure out an approach to make it work.

Its quite obvious, that you'll get zero time to automate if you start acting like an exploratory
tester on the team and shovel tickets through the JIRA pipeline for every change the dev makes. Thus
you need to have **open and honest conversations** about your bandwidth to your devs and leadership
and ensure **everyone on the team tests** so that you get more time to automate.

You should rather spend time in building out tools, frameworks and write automated tests as they
would definitely scale beyond you trying to do everything by hand.

I think this topic is a bit more nuanced and i'll maybe write more about this in a future post.

## Conclusion

I hope this post gave you some idea about the SDET role. This is my broad perspective about the role
and i'm sure there would be lot of macro level details that we could not get into in a single post.
Let's keep the conversation going and do let me know if you feel i've missed something here in the
comments below.

As always, Do share this with your friends or colleagues and if you have thoughts or feedback, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing and coding.
