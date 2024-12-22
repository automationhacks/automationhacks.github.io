---
title: "Dev: QA ratio A tale of burnout? Is there a better way out?"
excerpt: "A deeper look at disproportionately staffed engineering teams and what can we as leaders do to nudge this into more healthier and balanced directions"
permalink: 2023-12-31-dev-qa-ratio-a-tale-of-burnout-is-there-a-better-way-out
published: true
image: /assets/images/2023/12/dev-tester-ratio.jpeg
canonical_url: "https://newsletter.automationhacks.io/p/dev-qa-ratio-a-tale-of-burnout-is"
categories:
  - "Leadership"
tags:
  - "Software Engineering"
  - "Career growth"
  - "QA"
  - "SDET"
---

<figure class="image">
    <img src="assets/images/2023/12/dev-tester-ratio.jpeg" alt="Image showing few dev and testers collaborating over a whiteboard">
</figure>

A deeper look at disproportionately staffed engineering teams and what can we as leaders do to nudge this into more healthier and balanced directions

Recently, I’ve been reflecting on an important question in the testing space around building and staffing a balanced team of engineers

Let’s start by asking this question:

What do you think is the ideal Developer to Tester ratio on the team?

When I refer to the word **tester**, I’m broadly referring to a person who is a testing specialist and can own the entire thing E2E i.e. break down requirements into acceptance criteria, work with product managers (PM) / Business teams and developers to ensure the right testing happens throughout the life cycle. This person cares deeply about Quality and sets up the right processes, develops automation, test infrastructure, and tools to conduct and aid in testing, and if need be jumps in and tests things manually (_or exploratorily whichever term you prefer. I like to not discriminate_), triage bugs, publish status. So on and so forth.

You may refer to such a person as a QA, Test engineer, SDET (Software development engineer in test), SET (Software engineer in test), SETI (Software engineer tools and Infrastructure), etc. Take your pick. 😏. We should not let a [title define a person and their capabilities](https://automationhacks.io/2020/10/08/testers-identity-crisis/)

## What does the community think?

I posted the below question on LinkedIn hoping to get a sense of how my testing peers feel about this topic:

<img src="assets/images/2023/12/dev-tester-linked-in-post.png" alt="Linked In post" style="width: 75%; height: 75%; display: block; margin: auto;">

I was surprised to see this topic being something people resonate with and poured their thoughts into.

The post has 68K impressions, 319 reactions, and 39 comments. 30.4% of the viewers were from large organizations with 10K+ employees and 14.9 from mid-sized organizations with 1K to 5K employees.

![Post impressions](assets/images/2023/12/dev-tester-post-impression.png)

Some acknowledged the problem, others provided more context on how they operate in such an environment and others provided concrete and abstract approaches.

Please feel free to [read the comments](https://www.linkedin.com/posts/automationhacks_softwaretesting-qa-automationhacks-activity-7144389351060234240-2VNC?utm_source=share&utm_medium=member_desktop). There is some really good advice there and make up your mind about this.

## Ratios galore ➗

I knew from the start that the right answer to this question is highly subjective and depends on multiple factors like the team structure, the nature of the product (UI/API/Data heavy), and how much dedicated testing needs to happen by a testing specialist.

Please humor me and let's break this down and poke at it from different angles to understand the problem space better.

I’ve seen several numbers throughout my career for Dev: Tester ratios starting with a strict 1:1 mapping to the gap increasing quite steeply. At highly skewed rations software delivery operates in a completely different way.

- 1:1 (Extremely well-staffed system test team of the olden times)
- 3:1
- 4:1 (Quite a common no that folks advocate for and sometimes recommend)
- 6:1
- 13:1 (Anecdote: In my [initial days at Gojek in a feature team](https://automationhacks.io/2021/06/08/10-years-of-software-testing-automation#working-in-a-start-up-product-company))
- 23:1 (At WhatsApp, In a Test automation platform team)

It is super interesting to see that in each of the above contexts, The nature of Testing and who does what changes dramatically. Maybe we can explore that in a later post.

## What's the problem? 🤔

Let’s understand the problem a bit deeper.

The more skewed the ratio is, the worse it is for the tester and the team in retrospect.

Why?

Let’s look at it from the lens of a tester

Image you have a 4:1 ratio and you are the person supporting testing for a POD. It is quite a fair ratio if the dev velocity is reasonable and you are responsible for testing 1 or 2 stories at a time. If you are blocked on one, you can switch to the other and things move forward. Easy peasy.

However, in a more fast-paced team with lots of feature work being done, you may be looking at 5 - 6 items waiting on your plate to be tested.

These are the items:

- The product/business team wanted it to be shipped \_yesterday \_or ASAP. 😉
- The Dev has already done the dev work:
  - Wrote unit tests
  - Did a high level of sanity of the flow.
- They have probably already moved on to the next item on their backlog and also started losing context.

What could go wrong in such a scenario?

Say you have these 4 features on your plate:

- A and B are urgent and important features that are business-critical or unlock new revenue streams for the company
- C is not urgent but an important feature that may optimize efficiency.
- D is a good-to-have feature.

Like a street-smart tester who has a good bearing on the risk, you’ll judge and align on the priority of these tasks and stack rank the order in which you’ll pick them up.

How will you test? Probably you’ll do some of these activities

1. You’ll start to design cases
2. Get them reviewed, and publish them in the test management tool.
3. If a mature framework exists, you’ll start writing automated tests
4. If a framework does not exist, you will start building it or ask a relevant platform team to help you and go ahead with some workaround or hack.
5. Analyze any failures
6. Report bugs as they come up
7. Fix and maintain automated cases that fail due to legitimate changes
8. Look at any regression failures
9. Communicate status and timelines to leadership and stakeholders, etc.

_⚡Did you notice even in a very basic flow there are 9 distinct steps?_

Say Feature A gets a blocker bug, you log a bug report it, and give the necessary details to the dev to help them work on a fix.

In the meantime, Like a smart scheduling algo, You’ll pick up Feature B and repeat the above steps while completely switching context

Maybe the same cycle happens there as well.

You then either switch back to Feature C or pick up Feature D.

Also, do you spot other problems?

Now while you work on feature C, the other branches are getting stale, isn’t it?

For you to test something, the branch needs to be rebased with work that has already moved on (both for the automation code and the source code).

The dev may spend time resolving merge conflicts. Maybe they see some tests broken and fix them and finally they again 🫰 [“hand over” the build to you.](https://automationhacks.io/2019/06/24/testers-are-not-the-last-line-of-defence/)

You are already working on other features and ask them to wait a while or you retest and find another bug and find it's blocked again 🤦

The dev and their manager think argh! When will this feature finally ship? This may also build some friction and resistance between the 2 crucial functions and in case of tight timelines put a lot of pressure and increase anxiety.

Devs may try to get stack ranking to get their features prioritized and get quote-unquote your “testing cycle time”

Also, What about building long-term scalable tools and frameworks to solve these systematically? Where is the time for that?

God forbid. What if you have to take a vacation?

Phew! 😓

Let’s take a step back here! 🔙

Do you get a sense of what's happening here and spot some other problems with this setup? Let me know in the comments.

## The Bottleneck 🍾

In the above scenario, My dear friend. You as the tester have effectively managed to be the bottleneck in the delivery cycle, slowing down everything and royally burning yourself out in the process for no genuine fault of your own.

You are still someone who cares deeply about the quality of the product and wants to do N other things to improve it, but unfortunately in such a constant hustle and sense of urgency environment, you’ll never have enough focus time

Let’s also ground this a bit. While we assumed the worst in the above hypothetical (or oddly quite realistic scenario). It’s not always going to be this bad and your mileage may vary.

In some companies, product and dev may be patient and okay to wait until Features are well tested and have gone through. People are generally reasonable if you convey your perspective with the right data and argument.

Some features might not need deep testing and you may also be okay to cover the major acceptance criteria.

In short, Context matters.

I have a lot of empathy for both Devs and testers in such situations, and throughout my career, I’ve stepped into many of these shoes and seen things from both sides and different angles.

We need to solve this problem or at least move in the right direction of solving since left as is, this just leads to burnout and attrition and unhappy teams, and that's not what engineering should be right?

Where is the fun in that? 🤷

## What's the elegant solution here? 🥲

Alright!

We know what the problem is.

Let’s roll up our sleeves, put on our critical thinking and problem-solving hats 🎓, and think of some creative ideas on how to solve this.

If you think about it, at a basic level. This is a classic demand and supply problem.

- **Demand:** Product/Dev Need X hours of your testing time on a feature to make it something production-ready
- **Supply:** Tester’s time, experience/expertise, energy and creativity, etc

### Solution 1: Increase supply 🚰 → i.e. Reduce the ratio

One way to solve the problem is of course reduce the ratio

For the sake of argument, Instead of 4:1, we can make it 2:1, i.e. for a 16-member Dev team we have 8 testers and these are spread across different PODs to form [small Two pizza teams](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/two-pizza-teams.html)

Wow! An 8-member dream team! What would they do? 🤩

Glad you asked!

Maybe some of them do more dedicated feature testing work than others, some build dedicated frameworks and tools to provide new testing capabilities, some build Infra and monitoring, some take care of **Non-functional Illities** (Accessibility, Usability, Security, Load), some look at customer data and do analysis and aid in production bug triage and resolution or increase coverage.

This would increase the **slack** in the system, and while you may trade off 100% allocation and utilization of everyone’s bandwidth every day, you may be able to do more with the people you have and move faster. (Also, note that 100% extended utilization is just pointing to a CPU crash in the future. Just saying 😉)

This is just common sense at play, the more hands the better!

This would also enable leaders to build backups avoid single points of failure and have a more balanced team

What if 2 people decide to move on from the company at the same time?

Well, You still have folks to pick up the load in the interim while you search for lateral hires within or outside the company (which is famously hard). If someone has to go on a vacation or support their family in a medical emergency, no problem, you can pass on context to their backup and the show continues.

A larger team means Senior engineers can mentor less experienced engineers more closely and help them compound and ramp up.

This model could work as it seems quite healthy on paper. This is how much of the software was developed and tested earlier.

But … (Oh, the dreaded but!)

However, this model is not without its flaws

Unfortunately, In many modern teams, the perception of dedicated testing and QA is wrongly set as a Cost center. 😞

If you want to increase the dev headcount to 100 devs, you must staff 50 testers. You can see how at scale and in a large enough company, this does not scale.

This also encourages the tendency to hand over builds for sign-off, pass fixes over the wall, play bug ping pong, and some of the many dysfunctions that happen in the team when people tend to over-rely on someone else to bake quality in their product.

Couple this with management resistance to invest in this and voila we are bad to poorly staffed and unhappy teams! ⛔

### Solution 2: Keep supply the same, get devs to do more testing 🧑‍💻

> Scarcity of resources brings clarity to execution and it creates a strong sense of ownership by those on a project\*\*. Imagine raising a child with a large staff of help: one person for feeding, one for diapering, one for entertainment, and so on. None of these people is as vested in the child’s life as a single, overworked parent. It is the scarcity of parenting resources that brings clarity and efficiency to the process of raising children. When resources are scarce, you are forced to optimize. You are quick to see process inefficiencies and not repeat them. You create a feeding schedule and stick to it. You place the various diapering implements close to streamline steps in the process. It’s the same concept for software-testing projects at Google. Because you can’t simply throw people at a problem, the toolchain gets streamlined. Automation that serves no real purpose gets deprecated. Tests that find no regressions aren’t written. Developers who demand certain types of activity from testers have to participate in it. There are no make-work tasks. There is no busy work in an attempt to add value where you are not needed.
> ― James A. Whittaker, How Google Tests Software

I love this quote and analogy by James. If you’ve not yet read this book, I’ll encourage you to read it. You’ll get many more such nuggets of wisdom and it could be a start towards your book-reading journey as well ❤️‍🔥

This is a more practical approach that your management chain will surely love.

Now you as a tester might say, Wait, hold on a sec.

- You are asking me to trust a developer to test their code and ship it? Without me even involved, are you for real? Get out of here!
- What about their biases? Surely, they can’t find any errors or bugs in their own code.
- What if they are irresponsible and don’t test properly?
- What about edge cases and negative cases, what if they just test positive cases and move on?
- Also, What will I do if Devs do testing? Why do they need me?

You are right to bring these points up.

These are concerns that should be mitigated. These problems are deep and require someone with the brain space and the right motivations to tackle them.

That is you, my friend.

If not you, who else?

I hate to break it if this is coming off as a surprise, but as a person working in the Testing space, you have to learn how to see the bigger picture and play a bigger role in enabling and supporting teams to move faster. It’s not just who can bake or beat quality into a product. It's everyone's responsibility. This is not lip service. It is how modern software can be delivered at scale. And it takes a whole village to get there!

Some problems need to be solved at a grassroots and engineering culture level.

#### [Can devs test?](https://automationhacks.io/2023-07-09-meta-engineering-practices-engineers-write-tests)

The bias of devs not being capable of testing or automating is probably not right. I’ve found that devs are perfectly capable of testing,

They have written the source code. They obviously know how to code and given time, mentoring, and motivation from leadership can think quite critically about scenarios to write. The best developers I’ve worked with are always mindful of the gaps in test coverage and work diligently towards mitigating them.

The limiting factors are really time and incentives.

If a Dev is incentivized to ship code faster and move on to the next one. They might be inclined to do just **“good enough”** testing. If the culture incentives high-quality release and proper time in the project timelines for testing and bug fixing. Then there is still hope. Leadership really needs to be spot on and care deeply about quality.

So, In the previous hypothetical scenario with a 4:1 ratio staffed team with 16 Dev and 4 Testers, instead of 4 people doing Integration/E2E testing.

It's rather 20 people. 🫢

You can imagine how that would make things much faster and also help the 4 dedicated testing experts on the team scale.

#### What is the role of a tester in such a setup?

There could be multiple things you can do.

- You as the testing expert might handle big bet projects for the company directly
- Make sure the right testing strategy and plan is followed.
- You help keep devs accountable for testing and also serve as a coach
- Act as a builder and bridge to dedicated test tooling, frameworks, and Infra. Not everyone has the bandwidth to be up to date on all the latest tools being built in a company or the wider open-source landscape. A dedicated focus would help.
- You may also shift focus to building tooling and frameworks
- Creating correct views and finding insights that would help Devs test their features and code better.

These are big-ticket items.

Many big tech companies have multiple Infra / Engineering productivity / Dev experience teams dedicated just to this stream with a long and endless backlog of things to do.

Trust me, there is no shortage of work in this space.

#### 1st and 2nd order effects of this approach 🐎

This can have some 1st and 2nd order effects on a team's engineering culture and practice.

##### 1st order

- Devs would be more accountable for the quality of their code
- Devs are incentivized to carefully test and write automated tests since they don’t have a tester safety net for all their features.
- They may spot inefficiencies in the testing framework and help the test team build some of the tooling as well
- To get an unbiased take on their feature, another dev can pick up the story for dev and help test it, also leading to knowledge sharing.
- Since test coverage increases, teams will have more confidence to ship code and customer value faster (**without sacrificing quality**)
- The tester can help review testing plans for more projects and also partner and brainstorm on finding the right coverage.
- The tester stops being the gatekeeper.
- Testers may be able to explore nonfunctional and other types of testing than just feature work

##### 2nd order

- Teams can scale well without having to stick to a ratio
- More Testers' bandwidth means more time to build some of those efficiency and productivity improvement initiatives.
  - This creates a virtuous cycle 🌀 leading to more efficient testing.
- A dev team highly efficient at testing may not need many dedicated testing specialists. The testing specialists may then pick up some dev feature work or move on and help spread this model to other teams.
- A risk could be that testers may start to lose touch with the nitty-gritty details of some source code or features that were completely tested by devs.
- Devs not highly trained in testing may miss bugs.
  - This should be mitigated through an efficient release process and CI with multiple test runs in different environments, staged rollouts, feature flags, and monitoring to allow quick reversals if required. However, with this model, obvious bugs would not be missed.
- Testers may spread testing know-how in the team and help devs get better at it as well.

As some of you may know, many of the above have already been suggested by [Alan Page and Brent Jensen in modern testing principles](https://www.moderntesting.org/).

What does not get talked about as much is how to enable this culture in teams and shift in this direction and how we face and overcome challenges.

Hopefully, with this post, the conversation will continue in a more positive direction.

### Solution 3: DIY

There are very few Silver bullets in life and in testing space.

I encourage you to put on your critical thinking hats and figure out a path that works best for your team environment.

As you already know, Good advice and approaches taken out of context can create a lot of inefficiencies and may even turn bad.

So let me leave you with a final thought.

No matter how you structure your testing capability. What's important is that it is baked into your day-to-day engineering culture and there is continuous testing feedback at all layers. Fast testing signals towards the state of your product can be the difference between customer delight or a bad review on X or Google Play store and Apple App store. We should remember why are we doing the work that we do. It is grounded in the service of the customer and to delight them every single time and in turn, help our teams, and company become more valuable.

Whatever we have to do as a team to achieve that and to make our lives easier, balanced, and happy while doing it, we should do it!

Thanks for the time you spent reading this 🙌. If you found this post helpful, please share it with your friends and follow me (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time, Happy Testing 🕵🏻 and Learning! 🌱| [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
