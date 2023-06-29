---
title: "Engineering practices @ Meta: #3 Conduct an Engineering Bootcamp for new joiners"
excerpt: "Each new engineer @ meta goes through a 6-week intensive boot camp program that sets them up for success in their future teams and roles. Let's unpack how this experience looks like"
permalink: 2023-06-29-meta-engineering-practices-conduct-an-engineering-bootcamp-for-new-joiners
published: true
image: /assets/images/2023/06/thisisengineering-raeng-uyfohHiTxho-unsplash.jpg
canonical_url: "https://newsletter.automationhacks.io/p/engineering-practices-meta-3-conduct"
categories:
  - Engineering practices
tags:
  - "Meta Engineering"
  - "Software Engineering"
  - "Meta"
  - "Test automation"
---

Each new engineer @ meta goes through a 6-week intensive boot camp program that sets them up for success in their future teams and roles. Let's unpack how this experience looks like

<figure class="image">
    <img src="assets/images/2023/06/thisisengineering-raeng-uyfohHiTxho-unsplash.jpg" alt="A female engineer typing code on a multi monitor setup">
    <figcaption> Photo by <a href="https://unsplash.com/@thisisengineering?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">ThisisEngineering RAEng</a> on <a href="https://unsplash.com/photos/uyfohHiTxho?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a> 
    </figcaption>
</figure>

A long-standing pillar of Meta's engineering culture is a 6-week dedicated boot camp program that every new hire goes through. This intensive program typically ends with a team matching exercise where engineers can choose which product, infra, or other teams they want to be part of across either family of apps (FOA) like Facebook, Instagram, WhatsApp, Messenger or workplace, or Metaverse

This program is aimed primarily at onboarding software engineers on all the different internal tools used at Meta spanning from languages used for frontend, backend, and AI/ML development, to different data infra tools and multiple gigantic monorepos. This is obviously very necessary since the company has a pretty unique tech stack with tons of internal tools and frameworks.

This is also a caveat of joining meta initially since your existing open source tool knowledge is not immediately transferable and it takes some time (arguably even a year to be comfortable and productive with the entire ecosystem of tools)


### Get engineers to land their first change pretty fast 🏃

On day 1 of my boot camp, I remember pushing a modest change into the Facebook production app web page and seeing the changes before my eyes, albeit it was only a test webpage that only I could see. 

This is wonderful in its own right since just by doing this on Day one or two you very quickly allow engineers to get used to making a change via the IDE (VS Code), learn how to checkout an on-demand remote environment, go through the code review process, run a plethora of tests and see their outcome on CI systems and see all the quality gates. 

All the steps were well documented so that anybody without necessarily a web engineer background could follow these and land their change. You of course revert this change after becoming familiar with the E2E process. But I remember the feeling of doing this was very thrilling as an n00b engineer. If you were facing problems you could ask a dedicated workplace group called eN00bs

I think this could be a useful part of the onboarding program in any company. The act of tailoring it so that a new engineer could push a change pretty fast gives new engineers a lot of confidence. 


### My personal boot camp journey

When I personally joined Meta back in Nov 2021, I was given the option to choose an area where I want to boot camp in. 

There was no dedicated Quality or Testing track and there were 4 paths available to me at the time: Android, iOS, Web, and Server. In my former roles as an SDET, I had of course written a lot of code for automated tests or frameworks and [some APIs](https://github.com/automationhacks/people-api) before but had not necessarily been exposed to being an App, Backend, or Web engineer, so it was a bit confusing on what to really choose.

Each of these areas had its own learning path with the expectation that you'd have to watch videos, do some hands-on exercises, and also pick a new task to work on during that time. 


#### A backlog of bootcamp tasks

The boot camp program has an open backlog of tasks in an internal tasks tool that you could pick up with complexity indications, they start from L1 (Small change i.e. change a few lines), L2 (Modest change i.e. change a file), L3 (Refactoring or changing multiple files), L4 (Build a small isolated feature), L5 (I don't remember but probably build a complex feature). 

These tasks are created by different engineering teams within Meta, often these are tasks that either fit a particular pattern with pre-existing examples that a new boot camper could leverage or quite simply tedious work that engineers don't have a lot of bandwidth to tackle.

Why is this useful?

Well, boot camp engineers in the process of boot camp get exposed to different codebases or repositories within Meta and this supplements their learning experience. 

They also connect with the engineer who wrote the boot camp task and get experience in talking with different teams/engineers and building rapport. In case that team is hiring, this problem-solving exercise may even materialize into the boot camp engineer actually joining that team.

During my interview loop, I was spotted and pre-allocated to the WhatsApp Test Automation Infra team that worked on building test infra for WhatsApp mobile clients, and since I had some prior experience with Android automation, I chose that as my focus area and while I picked generic testing related tasks from the boot camp backlog like add tests, refactor testing frameworks, I switched to doing specific tasks for the team that I was allocated on and use the opportunity to connect with some other senior engineers on the team.

I had a lot of fun initially understanding how to build the Fb android app and learning different Android development constructs and their applications within fb stack. I also explored a few data tools within fb that proved to be quite useful in my time there later on as well.

Since I was pre-allocated, I did not have to worry about talking with hiring managers on different teams and had a pretty relaxed boot camp experience but I observed a few other peers speak with multiple managers, and sit with those teams to figure out if that teams specific culture worked for them as well. 

Overall giving this autonomy or choice to the camper is a pretty good move IMHO and definitely contributes positively to the company culture.


### You are not _generally_ alone, boot camp mentors are there to help!

Engineering Bootcamp programs are facilitated by boot camp mentors. Typically a mentor takes on 2-3 mentees. They are experienced engineers who are well-versed in Meta's engineering culture, tooling, etc. They help ask any questions that boot campers may have, help in finding appropriate tasks, keep accountability on the camper, and even navigate conversations with prospective managers who would want to hire those campers on their teams

The boot camp program also created a cohort of 3-4 individual campers who are also going through the process regardless of them being in Engg or other functions. This is a useful support system and helps new engineers build community within the company and some new connections. 

I've observed that this is also an opportunity for the boot camp mentor to get an idea of how to manage people directly and get credits on the people's axis of the performance management process. Most often these formal boot camp experiences also turn into longer-term mentor-mentee relationships as well. 


### Lots of fond memories

Overall, My first weeks in meta boot camp was a time that I have fond memories of and I feel creating something similar albeit small could be a positive addition to the engineering culture. As a bonus, here is a bonus article by the current CTO [Andrew Bosworth (boz) way back in 2009](https://engineering.fb.com/2009/11/19/production-engineering/facebook-engineering-bootcamp/) taking about the boot camp program

Do you have a similar program in your company? If Yes, Let me know in the comments.


Thanks for the time you spent reading this 🙌. If you found this post helpful, please share it with your friends and follow me (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time, Happy Testing 🕵🏻 and Learning! 🌱 | [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
