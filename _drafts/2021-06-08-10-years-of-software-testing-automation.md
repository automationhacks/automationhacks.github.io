---
title: 10 years of Software testing and automation
excerpt:
  "I started my career in Software testing and test automation 10 years ago on this very day. This
  post is me reflecting on how this decade went and some of my learnings and experiences along the
  way"
layout: post
permalink: /2021/06/08/10-years-of-software-testing-automation
image: /assets/images/2021/06/undraw_career_progress_ivdb.png
categories:
  - "Test automation"
  - Testing
tags:
  - "Experience"
  - "Advice"
---

![Career progress](../assets/images/2021/06/undraw_career_progress_ivdb.png)

Source: Illustration created by Katerina Limpitsouni on [Undraw](https://undraw.co/)

Today, 8th June is a special day for me. It's the day that I complete 10 years as a Professional
Software tester and automation engineer.

This long post is a trip down memory lane where I call out some of my key personal and technical
learnings, experiences, challenges and career highlights.

> Disclaimer: This is a gonna be a pretty long one, since 10 years is no short time! Grab a drink or
> popcorn 😉

## How I got into Software testing

It was a bright day in 2011 when I joined Accenture, my first Tech company fresh out of college with
an engineering degree in Information Technology. The vivid memories of that day are still quite
fresh in my mind as I remember going through the onboarding process.

I had no clue about which role, team or skill i'll work on in my career. Ever since college I wanted
to be a **Developer** and had built simple MS .NET and Java websites as part of my college projects.

I liked to code and felt a certain charm towards the role, even thinking of it as an elite role to
have at that point

My employer did a random skill allocation upon joining and I saw my skill was going to be
**Functional testing**. With no clue about what kind of career could be made in Software testing, I
was honestly a bit disappointed at that point and inquired on whether I can change my skill, I got
to know however that I can change the skill only after spending 18 months with the company/project
that I get enrolled in 😲

### A first taste of Software testing

Accenture had a green field training program where freshers would be trained on their allocated
skills and I was trained for a couple of months on HP QC (Quality center), HP QTP (Quick test
professional) using VB Script, Load testing using HP LoadRunner and a foundational knowledge of
different types of testing

At that point I was surprised to see that `"Okay, even Software testers code?"` 🤷 There is
something called as **Automated testing** that provided testers a way to automate away bulk of their
testing. I came to learn that testing is not about clicking some buttons around but involves
different flavours like **Functional, Non Functional, Security, Accessibility, Usability** and you
can go deeply into any of these topics

I remember saying to myself, **"hey, this looks really interesting, Are you telling me that i get to
do all that on a project 😆, seems like quite a challenge"**.

After completing my training successfully I joined the ARISTOS DSL team within accenture that built
solutions for a major US Telecom client.

> Learning: 💡 Software testing is not just clicking some buttons (as is commonly misunderstood),
> but a holistic field involved in checking if the system works at all of its different layers. It
> involves not just understanding the system deeply but also writing cool automation to make this
> whole process faster

## Hands on Test planning, execution and automation

I was fortunate to have really good and inclusive mentors who took me under their wing and showed me
how the process, of designing a Test strategy happened, How to write detailed test plans with
expected scenarios, conditions and results, How a scripted test is written covering the application
and the tracking entire execution/defect cycle on a test management tool

### Experiencing the thrill of becoming a bug hunter

I really started to enjoy the process of investigating the application and the underlying database
structure, infrastructure and while initially followed test plans created by senior engineers,
pretty soon ended up creating Test plans of my own.

Finding a bug and then getting it fixed by talking with Devs gave me a kick, knowing that the
product is better off and I'm directly contributing to increased customer satisfaction 👍

I also learned first hand how Developers, Testers and Technical/Business Architects, Design and
other functions, work all together to deliver quality software. Those were the days of long running
projects and structured change requests.

### Automating tests in QTP

I also realized that while the process of exploratory testing was very interesting it took me a long
time to run these cycles manually. My Test lead and manager wanted to see if this could be
automated.

I started to write **Test automation using QTP**, initially using record and playback feature of the
tool to write data driven E2E scenarios on the application. They were flaky as hell since every time
the website changed, I had to go back and modify the identifiers in the **Object repository**, it
was painful to do this and I wondered if this could be done in a better way?

We had a senior engineer on another team who was more into VB Scripting and had written a keyword
driven framework wherein instead of using record and playback, each component was **Hand-coded in
VBScript**

After learning and trying this for my own project I found this to be very efficient as managing
tests was much easier.

> Learning 💡: While record playback technologies are good to understand the application and
> generate scripts quickly, its not maintainable in the long run and its better to take that
> knowledge and hand craft the automated suite

### Services and Load testing

After spending an year writing UI automation, I moved more towards using **SOAP UI for Web, services
testing** by hand and again it was fascinating to learn since there was no UI to play with and you
can run functional tests quite quickly using them

> Learning: 💡 API testing is another way to verify functional and non functional aspects of the
> system and is much faster and more reliable to conduct than UI testing

I also got a chance to transition to a team that was running load tests on the application using
**Apache Jmeter** and I realized this was a quite different aspect of testing.

I mostly ran these tests and collected metrics while assisting an experienced Performance engineer
and communicating with infra teams to ensure once the System test phase was done, that our
application also performed well under expected load parameters

### Becoming a mentor

Towards the end of my time with Accenture, I had transitioned from a fresher to a more experienced
engineer and mentored multiple people who joined the team

I found the whole aspect of teaching someone on the team made myself learn things a lot better and I
had lot of fun talking with them, learning from them and enjoying countless team lunches and
outings.

## First Job change

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

### Building Web UI automation framework from scratch

After spending a considerable amount of time building API frameworks, I did a POC to build a
Selenium Python based framework for web automation. It was a challenge since I had never worked with
Selenium before and I read the code from another team and tailored their framework for Planview
team.

The learning experience was immense. I got to implement Page object pattern and learn Pytest as the
test runner of choice while also setting up CI on Jenkins and a local Selenium Grid setup on docker.
Taking on this E2E undertaking while learning how these technologies worked really gave me
confidence in my skills as an Automation engineer, I then mentored and on-boarded couple of other
engineers onto this framework

> Learning 💡: Using/contributing existing frameworks is great but you should really challenge
> yourself to understand how the different framework pieces work together and build stuff. The more
> you do this, the better you get with passing time

> Learning: 💡: Also, reading others code is a quick way to improve your craft as a Software
> engineer, the insights that you gather are invaluable

### Taking notes

I saw one of my senior colleagues had this practice of taking notes, whether it be tidbits to solve
a problem, snippets or even more varied notes. He was able to access these notes on demand easily
and this inspired me to maintain a healthy note taking habit myself. I experimented with different
tools like Evernote, MS OneNote, Notion before finally landing on Plain text note taking in Markdown
files

> Learning: 💡: Being able to take detailed notes and maintaining a second brain is very important
> for an engineer as it ensures that no solution approach is lost. Our brains are meant for creative
> thinking and not really information retrieval.

### Attending my first ever Automation conference

I remember attending my first ever Testing conference, Selenium Conference, Bangalore in 2016 and
was awestruck seeing such amazing and knowledgeable speakers including Simon Steward, Dave haeffner,
it was a great learning experience and I wondered how it would feel like to know enough to deliver a
talk in front of so many people

> Learning: 💡: Try and attend tech conferences, you often would learn about lot of new tips,
> approaches, tools and techniques, thought patterns about things that you either know currently or
> that did not know

## Working in a Start up product company

It was 2018 now and I saw one of my college friend post messages on facebook promoting his current
employer `Gojek`, while things at my current employer were excellent, I was a valued member of the
team and still had lots to learn, I wondered how would it be like to work in a Hyper scale product
company that creates so much social impact in the lives of South east asian people

I got a referral and after interviewing with them, realized that Gojek could be my next home. Gojek
had consumer facing apps on Android and iOS and a primary Java based automation stack using Appium,
Cucumber, TestNG and RestAssured.

I saw this as a opportunity to learn and grow myself more by understanding the challenges with
mobile automation and well as learn a popular static language like Java and joined Gojek in Feb 2018

### The challenges of working in a small team

When I joined gojek, I could instantly sense a change in pace, we had Bi-Weekly mobile releases that
required regression runs on consumer apps to ensure nothing broke for our customers and my team had
only a single QA consultant from consulting company. There was 0 app automation and the API
automation done by another engineer (who had left the team) was not managed and broken. We also had
a very less QA's as Full time employee and I was the 3rd QA in the bangalore office. 🤯, we did have
a large QA consultant team taking care of quality and automation in different teams though

The team was also going through the process of redesigning the app based on latest design language.
I remember thinking to myself, Wow, there is so much that I can do here. I started building context
about the team, the apps, backend architecture as well as existing automation frameworks

### Building Mobile Android UI automation

I first decided to improve upon the bottleneck of having to do slow manual testing cycles on mobile
apps for the Bi-Weekly FCT (Full cycle test) and started exploring the `optimus` framework which was
built by a consulting company called Test Vagrant. This was good since I got to read code from other
seasoned automation engineers and since I was grokking Java at the time, having this structure be in
place really helped

It was also quite a lot of fun to learn Appium's API with which I found myself quite comfortable
since it resembles the Selenium API quite closely due to it following the W3C WebDriver Spec quite
closely.

Learning this framework architecture as well use of Cucumber feature files was an interesting
challenge, and within a month or two I had a test suite in place to run against the Consumer Android
app on mac mini's with Gitlab CI runners, I did this in parallel to ensuring that the app redesign
release went fine and this suite reduced a lot of the manual testing effort that I had to put in for
this regression cycle

> Learning: 💡: If its boring and repetitive, automate it 😉

### Building API automation using Kotlin, TestNG

After an year of working on mobile automation, I had another colleague join from a consulting
company and I on-boarded him on the mobile framework and wanted to set out and build the API
automation framework for the product group that I was working in.

We had an existing test suite that covered few E2E tests however these tests were coupled together
heavily and it was very difficult to follow the code. Also the tests often would fail and made it
very difficult to find the problem at hand.

We had an existing framework in Gojek over rest assured that many different teams were using, and
while initially I thought to write my own python based test suite, I realized after a week of effort
that integrating my tests/utilities for other teams would be very difficult since they were mostly
using Java based stack and I would have to write lot of bridge code using Jython or the like.

At this point, there were few developers who also wanted to contribute to the framework and
automated test suite and suggested to try using Kotlin as an alternative.

Kotlin at that point was already the most popular language for Android development and had already
been blessed by Google as so, After researching and learning the language I found, that not only
writing code in Kotlin was faster, but it also was a lot more concise and expressive than Java

I decided to use it as the language for my team and convinced my teammates of the same. It learned
it from Kotlin Koans and other courses on Udacity and more so on the job. Also, wrote a lot of blogs
on using Kotlin along with TestNG. I later extended this test suite to run for all geographies that
Gojek was in as part of an App unification project and reduced the suite execution runtime from 1.5
hrs or so to 25 mins by implementing concurrency via TestNG and Kotlin synchronization blocks.

### From Lone QA to becoming a lead and then an Engineering manager

For the first two years of my career at Gojek, I was mostly a **Senior IC (Individual
contributor)**, designing test plans and automation myself, as well as directly mentoring one
colleague.

Infact for some 6-8 months I was the only automation engineer on the team.

How did I manage to accomplish what i did with such people crunch?

Well, I mainly ensured testing happened in the team regardless of who did it. On our team developers
tested lot of their own features and were very supportive

I would usually pair with Devs on the most critical features, helping to brainstorm possible
coverage gaps while planning and building automation solutions and this simple model led us to
deliver many features to our customers with high quality

> Learning: 💡: Learn to trust people around you (in general) and more so if you are the only
> QA/Automation engineer on the team, You won't be able to gate keep every change, but can surely
> sensibly automate flows that add maximum value and give Devs the insights and tools to do more
> effective testing.

#### Becoming a lead

With Covid and work from home, our team had to ramp up to adjust to growing needs of the business
and the business decided to hire 2 more automation engineers, managing the hiring and then
onboarding process was tough but I along with another senior colleague were able to achieve this by
setting up well defined process, setting proper expectations as well depending heavily on
documenting the system. We did lots of pair programming and code review sessions to help the new
joiners become comfortable with the team

Being the senior person on the team, I was also asked to manage these colleagues directly, This was
a slight shift since while I had lot of experience mentoring and working with team members, I was
never really done direct people management before. I mostly managed this by setting shared vision,
setting up processes and offering an empathetic ear during 1:1's

#### Becoming a manager

Within 8 months of me directly managing a couple of engineers, I got promoted to being the Quality
engineering manager of the entire logistics product group. I must admit I had my doubts about
whether I should continue to pursue the path of Staff engineer or engineering management and though
the Jury is still out on what I would really like

I still felt that learning to be an Engineering manager could add more dimensions to my personality
as well as skills. The key difference that I feel is that now I can take a more active role in
shaping up the quality of the product by using multiple tools at my disposal all the while helping
my colleagues excel in their interest areas

## Becoming a blogger, Conference speaker and Technical course instructor

### Started blogging

Around May 2018, I picked up another habit of listening to multiple podcasts on the bike ride to
office and I started with
[The stack overflow podcast with Jeff Atwood and Joel Spolsky](https://stackoverflow.blog/podcast/)
and really enjoyed their conversations around how Jeff was building stack overflow and the
challenges in scaling it.

I also started following and reading their blogs and felt an immediate connection with Jeff's
writing. There were many engineers in Gojek who had their own personal blogs as well as blogged
heavily on the company blog site. I thought to myself, blogging seems really interesting, maybe I
should give it a shot.

There were many inhibitions that I had in my mind, whether anyone would read it?, what kind of blogs
would i write? Jeff calls some of these fears out in
[Fear of writing](https://blog.codinghorror.com/fear-of-writing/)

Though, Instead of overthinking it, I just started with it. Setting up a blog on Wordpress was
really not that tedious, I decided on **automationhacks** as a name, since at that time I was
reading some blogs on **life hacks** and found that interesting tidbits and insights into solving
problems really saved a lot of time. Also, I wanted this blog to capture a breadcrumb trail of all
my learnings over the years while solving different problems.

> Learning: 💡: Blogging about your learnings is a really cool way of firstly understanding it
> better yourself, plus you other people benefit a lot by hearing different perspectives about
> solving similar or different problems. If you are in doubt, don't overthink, Just start 🏃

### My first conference talk at Appium Conf

It was around Jan 2019, and I saw the CFP (Call for papers) for Appium conf open. As I mentioned
before I had one goal of delivering a technical talk at a conference. I spinned up a CFP not knowing
whether it would be selected, but still by now I had realized its better to try and fail rather than
not try at all. To my surprise, my CFP was selected and I delivered my first ever talk in-person in
Appium Conf, Bengaluru. Wow! I had a great experience and met world renowned engineers like Angie
Jones, Jonathan lipps, Wim Selles, Jason Huggins in person. These people are regarded as legends in
Test automation space and I was a speaker along with them. 🙌🏼

### My first tutorial course: Visual validation using Applitools

I had heard about Test automation university and got a chance to talk to Angie Jones in person
during AppiumConf, I asked how can I help with this awesome initiative? Based on my python
background, Angie mentioned they needed a course on Applitools Python SDK. To be honest, at that
time I had not tried visual testing hands on but I signed up, knowing fully well that I could learn
on the go. 😉

> Learning: 💡: When someone says, can you do something? Say yes! And then get busy figuring out how
> you can do that. In other words. Fake it till you make it!

I followed Angie's tutorial on Applitools with Java and extrapolated it to Python language by
reading the Python SDK docs and created the course. The recording for this happened in the Gojek
office in early office hours over simple Sennheiser headphones with mic and with QuickTime and
iMovie as editing software (since I did not have a quite environment at home). I got useful feedback
from Angie during the production process and I learned so much about producing video content.

After finishing this course and seeing my name live on the site among many other world renowned
instructors . I could not have felt more proud of myself.

> Learning: 💡: Most of the things that you want in life, could be achieved when you put yourself
> into uncomfortable situations and by talking and working with other people

### Speaking at Online Automation Guild conference on Contract testing

Coming fresh from my first talk, I wanted to try my hands at different conferences and I saw CFP for
Automation Guild being run by Joe Colantonio, I had been a big fan of Joes podcast **Test talks**,
now called **Test guild automation podcast** and decided to try that.

I remember hearing from someone in a ministry of testing podcast that one of the best ways to learn
something new is to give a talk on it. I had heard about **Consumer Driven Contract testing** but
really wanted to learn it and see if thats something I could use in my own team and company

I proposed this as my topic and again to my surprise was accepted as a speaker. I prepared and
recorded this talk while learning and building knowledge on **CDC using PACT** in gojek offices on
weekends and my recent experience with building a course really helped since I was familiar with the
process.

During the actual talk and post talk slido questions, I heard about a lot of interesting questions
and they also helped me understand what aspect of CDC I needed to learn more

> Learning: 💡: One of the best ways of learning something is to teach it to someone else

### More talks and courses

I later on went to give another talk during Selenium Conf Online 2020 on "How to build an automation
framework with Selenium: Patterns and practices" and built another course on API testing in python
for Test automation university

## Any regrets?

## So whats next?

Where do I see myself going next from here?

TBH, I am not the type of person who would plan out next 5 years. I usually do planning for no more
than the next 3 - 6 months and a vague idea of the sort of things I want to try out.

Even though its been 10 years for me, I still feel like a beginner with a hunger to learn and
understand how different technologies work and what patterns could scale products as well as teams,
so I guess i'm just going to keep moving on in this journey.

Who knows, I might even start a YouTube channel, podcast or write a book. I know for sure that its
going to be exciting one.

The end... Or a new beginning 😉!

PS: If you read this whole post, I hope you could gather something useful from it. Do share your
experience in the comments as well.

As always, Do share this with your friends or colleagues and if you have thoughts or feedback, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing and coding.
