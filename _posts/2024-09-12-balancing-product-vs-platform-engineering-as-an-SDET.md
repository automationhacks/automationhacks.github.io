---
title: "⚖️ Balancing product vs platform engineering as an SDET️"
excerpt: "Strategies and tips on how to approach platform engineering work while working in a product team as an SDET"
permalink: 2024-09-12-balancing-product-vs-platform-engineering-as-an-SDET
published: true
image: /assets/images/2024/09/product-vs-platform.png
canonical_url: "https://newsletter.automationhacks.io/p/balancing-product-vs-platform-engineering"
categories:
  - Software Engineering
  - Career Advice
tags:
  - "Software Engineering"
  - "Advice"
  - "SDET"
  - "Platform Engineering"
---

<figure class="image">
    <img src="assets/images/2024/09/product-vs-platform.png" alt="Image showing a man on a balancing scale with a laptop in his hand">
    <figcaption>Created by microsoft copilot using DALL.E 3</figcaption>
</figure>

Any SDET working on a product team faces this

Does any of the below sound familiar?

“We _want_ to focus on building tooling/frameworks and infra to enable everyone on the team to test better but we don’t have the bandwidth to build this out”

“Our current setup is sub-optimal, we need things to improve, but also need to deliver on projects X, Y, and Z which are critical and time-sensitive priorities for the org”

“This is part of your core competency and expectation as a senior engineer and you must dedicate X% of your time to this”

“I feel overwhelmed and burned out and just don’t have the time for this, can we set realistic expectations”

“There are tons of meetings every day, how can I ever have time to work on this?”

“We cannot use BAU as a reason for not working on this”

Sounds familiar?

Some of these may be strong statements, but you get the drift.

## Is this a problem? 🤔

Yes and no! 😏

If you are an SDET embedded in a product team where there are always next projects or priorities lined up for you and your company also has expectations around product engineers doing platform work as well, you are surely going to be in this situation at a certain point in your career

An interesting side effect of this is that SDET on these teams **almost start to feel guilty** for not being able to do platform engineering work, leading to a false sense of degraded job satisfaction, lack of motivation, and unnecessary friction toward product testing work

Many engineers feel a strong pull and must work on more cross-cutting problems.

Some do seem to find the time to do it as well. What are they doing differently? 😖

Before we peel more layers of the onion, let's define what we are talking about here first

**What is platform engineering?**

It has many names within the software testing space that I’ve come across like test infra, engineering productivity, Testing center of excellence (CoE), etc…, but the idea is quite simple at its core

Engineers build testing tooling, frameworks, and infrastructure to help everyone test better thereby increasing shipping velocity without sacrificing quality.

This is interesting work and is also highly valued in many big companies depending on whether leaders recognize the value of infra and tools. They know even a small productivity gain for engineers can compound massive savings and speed boosts.

It's sexy because it is complex and challenging with opportunities to learn and develop deep skills as a generalist software engineer. Who would not want to work in this space?

Also, What could this work look like in practice?

One month you may be building bespoke tooling for a specific org problem or another month solutions that are more cross-cutting spanning code coverage, mobile device management, Test observability, CI/CD pipelines optimizations, intuitive frameworks on the backend, frontend (mobile, web), general test tooling for data setup, test environment isolation, etc

The list is long.

The role demands **dedicated bandwidth**, which unfortunately our engineer in this situation does not have

Many companies have realized the simple fact that this is a different kind of work to product engineering work and build dedicated specialized teams to work on these and then evangelize solutions to other teams.

Such teams gather feedback and then keep on iterating, hopefully making things seamless over some time. Since the nature of the work is quite ambiguous without clear ROI many times, leadership may find it difficult to justify investments in this space as well.

But, I digress. That is a tangent for another time.

Let’s come back to our original issue.

## What can you do? 🫢

Now that we have ample context about the problem

Let’s explore some solution spaces

### Product work is not all bad

How you think about a problem matters

I think we need to change the narrative a bit.

As an SDET, we are **accountable** for the quality of a given feature/group/service, etc. It is our core job role to ensure anything that is shipped is of high quality and delights the customer.

Efficient testing at scale is one clear lever you have but there could be other ways as well like getting devs to help out and own a larger chunk of test authoring, doing mob testing, building automated solutions that can run continuously and provide rapid feedback as you tackle increasingly complex problems

At the end of the day, You should remind yourself that your role is really in the service of the customer.

You are here to act as a force multiplier and get everyone on the team excited about testing.

You will need to be on top of changes, immerse yourself in context, attend meetings, influence the product roadmap, and of course handle the entire QA cycle of test planning, design, execution, automation, reporting, and bug life cycle and occasion prod issues

Before graduating to platform engineering, you need to be excellent at all of the above.

Please remind yourself that this work is what product, business and leadership care about.

You have to make peace with this situation and dedicate a large part of your day to ensuring that this objective is served. This is full-time work and you should never feel guilty for doing this

But …

We need to look further as well right?

### What about platform engineering work? 🧰

If you think about it

You practically have three options infront of you

1. Move to a dedicated platform engineering team 🧑‍🤝‍🧑
2. Make focus time in your day-to-day job to work on platform projects 🧑‍💻
3. Join/form a community and do things bottom-up 🙋

#### **Move**

The 1st option is a no-brainer, in the short term, it may be difficult to materialize but works out better in the longer term.

If you can move to a team whose sole charter is to focus on platform engineering work within testing

You will have all the bandwidth you need to pick the right problem and work on it

The funded team will have a clear charter and roadmap, a set of problems they are solving, and automatic leadership buy-in.

It's also a little scary once you shift your mindset from product engineering to platform engineering. You’ll realize the patterns and mental models you have in one do not translate immediately to the other.

You will need to acquire and build broader and more generalist software engineering skills. Also, develop awareness about different tools and technologies and the right problems to solve. This role requires judgement, communication, and external awareness to identify industry solutions and approaches to problems as well

These like any other skills can be learned to a degree, but you need the right approach, growth mindset, and the willingness to put in the time hopefully with some experienced mentors

#### **Make the time 🐸**

If option 1 is not feasible, because your team does not support internal mobility or such a group or team does not exist itself.

What can you do then?

You should first align with your manager that you want to spend **X%** of your time on platform engineering work. In my experience asking for 20% is fair. If you think about it, it is 1 day in a week or 2 hours every day for a 40-hour work week and usually a small enough period that other stakeholders in your team will not even notice.

If your manager does not care or is too much in a firefighting setup all the time. You may have an environment that is not conducive to this and then it is time to evaluate other options

But assuming you have alignment

When was the last time, you blocked your calendar and sat heads down to work on solving a platform problem?

Think about it for a moment, before you read on.

In my experience, time blocks on your calendar that you protect almost like a hawk are helpful. If you ensure to work without any distractions during this time, chances are you will make some progress for sure. People refer to this as “Eat the frog” i.e. work on the toughest part of the problem first thing in the morning when your mind is fresh.

This of course requires discipline and changing a few other habits as well like mindless doom-scrolling slack messages without really getting much signal among endless noise and chatter

I usually turn off notifications, kill Slack or other messaging apps, put on DND on my phone, and then get right down to business. Time block helps a little in mitigating Parkinson's law since time-bound tasks tend to get finished than unbounded tasks.

Another tip would be choosing your personal time of the day when it's less chaotic and people are not demanding of your time will work better, so either earlier in the morning or later in the afternoon, or early evening. It depends on when you are more focused.

Go on, Try it, trust me it works wonders!

#### **Community 🤝**

Do you have to be the hero who saves the day alone and gets all the credit?

Well, No. ⛔

That is not how modern teams work

You may still choose to do it, but you’ll have a tougher road ahead getting people to adopt whatever you choose to build.

Instead, one alternative could be to form a community of like-minded peers

Talk to your peers and get a few other engineers excited about solving a problem, and then figure out times in your schedule to work on it and solve it.

A small 2 pizza bottoms-up team can work wonders. You don’t need a lot of folks, just people who are really motivated.

You get bonus experience in leadership, community building, and building deeper relationships with peers either in the same team or beyond your team as well. It's a win-win!

This kind of organic initiative is something leadership usually likes a lot and it's also good for your career growth within the company since you build the org and make it stronger by opening up mentoring opportunities.

Oftentimes more than the work, investing in building meaningful relationships may have an outsized long-term impact on your careers

You just may make a workplace friend as well as another bonus. 🤷

## Fin 🐠

I know I did not solve your problem

But hopefully, it gave you some ideas on how to think about this in your day-to-day and perhaps some approaches you can try.

Go ahead and try your own experiments, some may just work out. 😉

Also, if you have faced this, how have you solved this in the past. Let me know your thoughts in the comments.

Thanks for the time you spent reading this 🙌. If you found this post helpful, please subscribe to the substack [newsletter](https://newsletter.automationhacks.io/) and follow my YouTube channel (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time 👋, Happy Testing 🕵🏻 and Learning! 🌱| [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
