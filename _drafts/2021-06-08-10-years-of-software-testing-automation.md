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

After 3 years 3 months with Accenture I decided it was time to move on and change jobs and see how
other projects and teams were solving similar or new problems.

## Testing an analytics product

I had an offer from an early stage startup and a more stable enterprise company and decided to join
Aricent (now Altran) as my next employer in September 2014.

I joined Aricent as a Senior Engineer - Testing in the Itron Analytics team which was responsible
for building analytic dashboards for Gas, Water, Electricity meter for a big utilities company in
US. When I joined the QA team size was 4 including a people manager.

It was exciting since I had previously not worked with analytics product and I got to understand how
complex ETL processes would take data and seed and aggregate Data ware house tables. Pretty soon one
of my seniors left the job and I became to most senior IC on this team.

I learned how to design test strategies for this complex product and also participate actively in
all Agile ceremonies between a cross functional team across India and US. Understanding how a tester
can effectively help shape product direction by calling out missing requirements, clarifying
acceptance criteria and help team improve by bringing up process inefficiencies in Team wide retro
was a lot of fun

### Building UI automation with Microsoft Coded UI

One of the biggest challenges in this team was when we decided to rewrite old legacy Flash based
dashboards with rich modern graphs using D3 and HTML5. The test manager on the team also decided for
us to use `Microsoft CodedUI` as the UI automation framework since we were heavily into Microsoft
stack (Visual studio, C#, TFS (Team foundation server), and MTM (Microsoft test manager)). I also
got a chance to travel to USA to San Francisco, California and Spokane, Washington along with a
colleague to help test and deliver this migration feature

Coming from my QTP/UFT background, it was a challenge to understand `C#`, `CodedUI` technology
however I was able to learn these and become a productive IC on the team under a more experienced
Lead. `CodedUI` heavily encouraged use of Hand coding while building the framework and I remember
making use of `Hexawise` tool to generate lot of data combinations which formed the basis of our
regression suite

> Learning: 💡 Don't be bounded with the Tech stack that you are used to, learning a new automation
> stack helps you to become a more well rounded Automation engineer

## Working in a small sized company

After contributing to this teams success, I wanted to move on to a more challenging role and
switched jobs to **Projectplace India** which later was acquired by **Planview USA**. We had a team
of 3 Automation engineers in India that grew to 8 people in some months time.

This role required to learn `Python` for test automation and looking back joining this company was
one of the best decisions I took.

My colleagues were all 10+ years experienced and I learned so much from their existing knowledge
while being challenged on an individual level.

### Building API automation frameworks with scratch

We liked to call ourselves the `Jedi` team, a name i proposed driven from my fondness for Star Wars
trilogy and we augmented a largely manual QE team in USA by building automation tools and frameworks

I got a chance to contribute to building a framework that used Microsoft PICT tool for generating
pairwise combinations to test SSRS (SQL Server Reporting Services) analytics reports and performed
XML comparisons against a set baseline. This also stored these test results in SQL Server database
and had an in house dashboard to present these test results while using Jenkins for CI. Seeing a
rich framework built from scratch and contributing hands on was a dream come true

I still remember, the India head come over to my desk early morning and calling out the importance
of treating oneself as a Software craftsmen and taking pride in being a solid engineer and building
these reusable solutions to make QE more efficient. Coming to office every day and coding till
evening while building automation was very addictive and I believe everyone needs to go through an
experience like this

> Learning: 💡 Working in small teams and companies can really challenge you and ensure you learn
> and grow way faster than in enterprises

We also built a custom test framework to use SOAP, REST based APIs and check integrations between
different Planview and Projectplace products as well as external tools like JIRA, Rally etc.

I also got the chance to travel to Austin, Texas USA for a couple of weeks to understand more about
the product as well as conduct trainings for the QE team there on using and contributing to the API
automation solution that we had built in bangalore

### Building UI automation framework from scratch

After spending a considerable amount of time building API frameworks, I did a POC to build a
Selenium Python based framework for web automation. It was a challenge since I had never worked with
Selenium before and I read the code from another team and tailored their framework for Planview
team.

The learning experience was immense. I got to implement Page object pattern and learn Pytest as the
test runner of choice while also setting up CI on Jenkins and a local Selenium Grid setup on docker.
Taking on this E2E undertaking really gave me confidence in my skills as an Automation engineer and
I then mentored and on boarded couple of other engineers onto this framework

> Learning 💡: Using/contributing existing frameworks is great but you should really challenge
> yourself to understand how the different framework pieces work together and build stuff. The more
> you do this, the better you get with passing time

### Attending my first ever Automation conference

I also attended my first ever Testing conference, Selenium Conference, Bangalore in 2016 and felt
awestruck seeing such amazing and knowledgeable speakers, it was a great learning experience and I
wondered how it would feel like to know enough to deliver a talk in front of so many people

## Working in a Start up product company

It was 2018 now and I saw one of my college friend post messages on facebook promoting his current
employer `Gojek`, while things at my current employer were excellent and I was a valued member of
the team, I wondered how would it be like to work in a Hyper scale product company that creates so
much social impact in the lives of South east asian people

I got a referral and after interviewing with them, realized that Gojek could be my next home. Also I
was to join a rapidly growing product team which had only a Single QA consultant. Gojek mostly had
consumer facing apps on Android and iOS and a primary Java based automation stack.

I saw this as a opportunity to learn and grow myself more by understanding the challenges with
mobile automation
