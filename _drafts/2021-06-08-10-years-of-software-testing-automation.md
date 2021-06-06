---
title: 10 years of Software testing and automation
excerpt:
  "I started my career in Software testing and test automation 10 years ago on this day. This post
  is a reflection of how this decade went and some of my mental models around Software testing"
layout: post
permalink: /2021/06/08/10-years-of-software-testing-automation
image: /assets/images/2021/04/tau-course.png
categories:
  - "Test automation"
  - Testing
tags:
  - "Experience"
  - "Advice"
---

Today, June 8th is a special day. It's the day that I complete 10 years as a Software tester and
automation engineer. This post is a trip down memory lane as well as calling out some of my key
learnings along the way

## I fell into Software testing

It was a bright rainy day in 2011 when I joined Accenture, my first company fresh out of college.
The vivid memories of that day are still quite fresh in my mind.

I had no clue about which role, team or skill i'll work on in my career. Ever since college I wanted
to be a **Software developer** and had built simple MS .NET and Java websites as part of my college
projects. I liked to code and felt a certain charm towards the role, even thinking of it as an elite
role at that point

However my employer did a random skill allocation on joining and I saw my skill was going to be
**Functional testing**. With no clue about what kind of career could be made in Software testing, I
was honestly a bit disappointed at that point and inquired on whether I can change my skill, I got
to know however that I can change the skill only after spending 18 months 😲

### A first taste of testing

Accenture had a green field training program where freshers would be trained on their allocated
skill and I was trained in HP Quality center (later becoming HP ALM), HP QTP (Quick test
professional) using VB Script, Load testing using HP LoadRunner and a foundational knowledge of
different types of testing

At that point I was surprised to see that "Okay, even Software testers code?" 🤷 There is something
called as **Automated testing** and that allows testers to automate away bulk of their testing. I
came to know that testing is not just clicking some buttons around but involves different flavours
like **Functional, Non Functional, Security, Accessibility, Usability**

I said to myself, hey, this looks really interesting, Are you telling me that i get to do all that
on a project 😆, seems like quite a challenge. After completing my training successfully I joined
the ARISTOS DSL team within accenture that consulted in building solutions for a major US Telecom
client.

> Learning: 💡 Software testing is not just clicking some buttons, but a holistic field involved in
> checking if the application works at all the different layers thats possible. It involves not just
> understanding the system deeply but also writing cool automation to make this whole process faster

## Test planning, execution and automation

I was fortunate to have really good mentors who took me under their wing and showed me how the
process, of designing a Test strategy happened, Writing detailed test plans with expected scenarios,
conditions and results, How a scripted test is written covering the application and the tracking
entire execution/defect cycle on a test management tool

### Raising bugs

I really started to enjoy the process of investigating the application and the underlying database
structure, infrastructure and initially following and then creating these Test plans on my own. And
finding good bugs in the system.

Finding a bug and then getting it fixed gave me a kick, knowing that the product is better off and
I'm directly contributing to customer satisfaction 👍

I also learned how Developers, Testers and Technical/Business Architects, Design and other
functions, work all together to deliver quality software

### Automating tests in QTP

I also realized that while the process of exploratory testing was very interesting it took me long
times to run these cycles manually. Even my Test lead and manager wanted to see if this could be
automated.

I started to write **Test automation using QTP**, initially using record and playback, using the
tools features to write data driven E2E scenarios on the application. They were flaky as hell since
every time the website changed, I had to go back and modify the identifiers in the **Object
repository**, it was painful to do this and I wondered if this could be done better?

We had a senior engineer on the team who was more into VB Scripting and had written a keyword driven
framework wherein instead of using record and playback, each component was **Hand-coded**, after
learning and trying this for my own project I found this to be very efficient as managing tests was
much easier

> Learning 💡: While record playback is good to understand the application and generate scripts
> quickly, its not maintainable and its better to take that awareness and hand craft the automated
> suite

### Services and Load testing

After spending an year writing UI automation, I moved more towards using SOAP UI for Web, services
testing and again this was very interesting since there was no UI to play with, I found out that
these enterprise apps make use of API to get data or do changes in the system and it was fascinating
to play with them.

> Learning: 💡 API testing is another way to verify functional and non functional aspects of the
> system works and is often faster and more reliable to conduct than UI testing

I also got a chance to transition to a team that was running load tests on the application using
**Apache Jmeter** and I realized this was a quite different aspect of testing. I mostly ran these
tests and collected metrics while working with an experienced Performance engineer and infra teams
to ensure once the System test phase was done, that our application also performed well under load

## Becoming a mentor

Towards the end of my time with Accenture, I had transitioned from a fresher to a more experienced
engineer and mentored multiple people who joined the team, I found the whole aspect of teaching
someone on the team made myself learn things a lot better and I had lot of fun talking with them,
learning from them and enjoying countless team lunches and outings.

## Changing jobs

After 3 years 3 months with Accenture I decided it was time to change jobs and see how other
projects and teams were solving similar problems.

I had an offer from an early stage startup and an enterprise company and decided to join Aricent
(now altran) as my next employer. I joined as part of the Itron Analytics team which was responsible
for building analytic dashboards
