---
title: Deep dive into evolution of testing organizations
excerpt: "Understanding how different testing organizations are setup in enterprise, small product, hyper growth scale up and big tech companies based on my personal experience"
permalink: 2022-11-10-deep-dive-into-evolution-of-testing-organizations
published: true
image: /assets/images/2022/11/undraw_Engineering_team_a7n2.png
canonical_url: ""
categories:
  - Testing
tags:
  - "Testing"
  - "Teams"
---

<figure class="image">
    <img src="assets/images/2022/11/undraw_Engineering_team_a7n2.png" alt="Image of 3 engineers having a meeting">
    <figcaption>
        Engineering Team by <a
            href="https://undraw.co/">Created by Katerina Limpitsouni on undraw</a>
    </figcaption>
</figure>

Hello there,

I have been a professional working in the software testing space since 2011 and during this time have been fortunate
enough to experience working in different testing organizations and setups in companies of different sizes.

In this post, I want to reflect on these different organization setups and what worked and what didn’t as I've
experienced them.

> Some of these setups still exist to date while others are relics of the past.

## Why read this?

This post might be interesting to observe and reflect on how the testing industry has shifted in the past decade through
my personal experience as a tester and if you are a leader in this space, might help you compare and contrast with
potentially some insights. I hope this is a somewhat interesting read.

Let’s go, shall we? 🏃

## Different types organization setups'

So what kind of testing setups exist?

Below are some variations I have experienced. This is of course not an exhaustive list but just what I have personally
experienced.

- A dedicated testing team that does manual testing and also writes _some_ E2E automation. Devs depend completely on the
  test team for functional testing.
- A dedicated testing team that does manual testing and a separate automation team that builds frameworks and tools and
  writes automated tests. Devs don’t write many tests.
- A dedicated automation platform team that builds frameworks and tools and provides these solutions to product teams.
  Devs write unit tests only
- A dedicated testing team that tests and writes automated tests as full stack test engineers and a community of
  practice that develops tooling. Devs only focus on unit/integration tests
- A team of QA leads that lead offshore contingent workers to get manual testing done, supported by a separate platform
  team that builds tooling, the Developer's own Unit, and UI test automation

Let me expand on these in the context of some of the companies that I’ve worked at.

## Dedicated test teams

### A dedicated system test team

![](assets/images/2022/11/testing-setup-1-system-test-team.png)

When I started my career way back in 2011 at Accenture as a Software Engineering Analyst, I was part of a dedicated
system test team.

Our client was a US Telecom giant and our team was responsible for owning the testing of an ordering system application
that was a set of Web UI that allowed customers to place orders and manage the entire order lifecycle for broadband
connections.

> While QA (Quality assurance) and QC (Quality control) terms were flown at that time as well, we used to call the team
> a “System test team” back then.

In this setup, The test team owned having an understanding of requirements, wrote test plans with scenarios, cases, and
scripts, and used to execute these plans manually for each release.

The project delivery was mainly waterfall which meant the team produced a major release every 3 months and supported
changes requests/hotfixes on a monthly basis and occasionally also supported testing for production issues.

The bulk of the work used our understanding of the application to design these test plans and execute regression
scenarios to support releases mostly by hand.

The other big chunk of work was of course finding bugs and tracking them to closure while talking to different XFN teams
(cross-functional teams) like business analysis, developers, infrastructure, and database.

The tester was a product specialist that was a cross between business analysts and end users and was called upon to give
ideas on what kind of tests to write or cover.

Deployments were done manually on VMs by the infrastructure team without much of a CI system being in place.

Developers did write some unit tests, and stubs to allow the Test team to test better but the entire effort for E2E
testing thru the different layers (UI/API/DB) was left to the “Test team” essentially establishing us as the gatekeepers
to give signals on when quality was regressing or discover any critical issues before releasing a build. So far all of
these activities are bread and butter for test engineers and should hopefully not come as a surprise to anyone reading
this post.

Our team also focussed on writing _some_ automated E2E UI tests using HP QTP (later called HP ALM) primarily using VB
Script mostly leveraging record and playback but also using dynamic scripting to make these scripts more robust. This
automation was run on our local machines and used to fail quite so often because of a lot of issues with underlying.
CI/CD were terms that had not gained that much traction back then.

There was no dedicated Automation team to support this automation effort and our team's attention was constantly shifted
between these different efforts (i.e. manual vs automation testing).

There were some teams that wrote load-testing solutions using HP Loadrunner and apache Jmeter but their
execution/monitoring was mostly done by hand and report preparation took time.

The push to automate usually came top-down from management since the manual regression cycle was weeks long and quite
inefficient and we wanted to reduce this time. Instead of focusing on meaningful coverage, automation became a means to
chase organizational metrics.

#### What was good? 👍

- A strong system test team meant good exploratory testing happened
- Devs found a strong partner to give them inputs on testing and test plans were discussed between business/dev
  partners. This led to better-tested features/changes

#### What could have been better here? 👎

- Manually testing features/bugs were quite slow and tedious
- Re-runs of the test suite were painful and often meant some bugs slipped through. It was very difficult to keep up
  with the pace of changes done by devs
- A small amount of UI automation meant the system test team was always overloaded between the dilemma to test manually
  vs automated cases since there were not enough cases to reduce the load.
- Feedback to devs was a function of the number of days it took the test team to execute the regression suite that was
  prone to errors
- Having to support automation without dedicated engineers to provide guidance meant that created automation was not
  very well designed and thus brittle.

### Yet another dedicated Testing team

![](assets/images/2022/11/testing-setup-2-test-and-automation.png)

Fast forward 3 years, It's 2014, and I joined Aricent as a Senior Engineer - Testing and started working on a client
project for Itron in their analytics team. The analytics group was rewriting their analytics dashboards from being
Flash-based to a modern stack using HTML5 and JS

These dashboards were used by energy companies in the US to understand and make sense of sensor data from Electricity,
Gas, and Water meters. A pretty critical application wherein wrong data could actually mean wrong signals that could
cause real problems for customers.

I was on the team responsible for ensuring the quality of these dashboards

For the first 6 months, the team was just 2 engineers and a manager and the job was to learn the app functionality,
execute the regression suite and add any new cases to it. These dashboards were quite legacy but stable in requirements.

There was 0 automation since it did not make sense to spend time automating flash-based dashboards when we knew this was
going to get rewritten pretty soon. This was probably the smart thing to do and saved a lot of effort being
unnecessarily wasted.

There was a frontend dev team in Bangalore that was tasked with developing the UI and the backend was handled by a dev
team in the US. Collaborating with the US meant being available for the office during off hours usually late nights in
Indian time.

There wasn’t any established good practice in writing unit/integration tests by devs and the project relied heavily on
the “Test team” to ensure the quality and accuracy of these dashboards, which sadly was done by manually preparing test
data, dropping it into appropriate locations for the ETL jobs to pick and verify the consequence on a dashboard or
database table. This was also of course slow, tedious, and quite painful to test since data aggregation was a complex
process and the team had to use SQL to verify it happened accurately.

#### A wind of change?

In the coming six months we had a leadership change wherein a couple of engineering managers from Itron US tried to
revamp this setup and bring a more Agile way of working to the team.

We started doing agile ceremonies like planning, grooming, standups, and retrospectives and this was great since it
brought a shared understanding of project deliverables and also opened up better conversations around roadmap and
feature development.

Later, We also hired a couple of experts in Coded UI automation and started creating a framework to automate the UI
using MS Coded UI with C#. Our client was already using a lot of Microsoft stack and technologies and thus sticking with
a similar stack was preferred, hoping devs could ramp up on the framework easily.

This was the beginning of a dedicated set of automation engineers (aka SDETs) who churned out UI automation cases and
these were run on configured VMs using MTM to orchestrate these runs. As an early member of the team I had become an SME
(subject matter expert) on the app and thus was able to provide good inputs on which cases to focus for automation while
also onboarding to the framework and contributing to writing automated cases.

#### What was good? 👍

- Using Agile was wonderful since it brought so much focus and structure to the feature development, it led to good
  discussions of features between India and US teams during grooming and planning and led to writing better acceptance
  criteria, having a 3W sprint meant features were shipped incrementally and thus delivering functionality in the hands
  of customers faster. All the good things agile promised!
- Establishing a dedicated team of SDET to write the framework and cases freed the test engineers to go to the app with
  dedicated bandwidth. Also, more cases being automated meant it reduced the testing cycles.

#### What could have been better? 👎

- Devs could have been onboarded to write E2E automated tests
- With little to no API, backend automation for an ETL-heavy system was a lost opportunity of writing good and reliable
  automation
- Lots of upfront repetitive manual testing was painful to do.
- Lack of knowledge sharing, SDET could have onboarded test engineers on the framework better

## A dedicated automation team

After 2 years or so, I wanted to try working for a company of a smaller size in the hopes that I would get to do more
things hands-on. I joined the Planview office (then called Projectplace which later got acquired by Planview US) in
Bangalore around 2015.

I joined as the 3rd founding member of the automation team in the Bangalore office and the major responsibility of the
team was to build test automation solutions and frameworks that could be used to speed up testing.

Planview was a work management tool that had most of the product development and testing teams in the US and as a
product was quite complex with tons of configuration options. There was a Quality engineering team in the US that was
testing the web app by hand and as far as I recall It used to take weeks or months to execute the entire regression
suite for releases. The testers in the US were mostly testing by hand and had little programming knowledge.

### Enter the Jedi team

Our team was the automation experts, I had the privilege to suggest the team name “Jedi”, showing my love for the star
wars franchise. The team started with 3 engineers and by the time I moved it had ramped up to 2 teams of 4 engineers
each.

We built multiple solutions such as a python based API integration suite to verify product integrations, A Pairwise
testing solution to test MS SQL Server Analytics reports, and later Selenium Webdriver-based UI automation framework to
test Planview Web apps run on Internal Selenium Grid on Docker. Most of these tools used Jenkins as a CI system and were
run on internal VM infrastructure.

Our platform team did not test the product by hand and relied on the QA team in the US for functional expertise and
drive priority towards automating cases. Each solution was treated like a product wherein we would take requirements,
develop and test it and then hand it to the US team to use/run and ease their testing tasks along with solid
documentation.

US Devs were mostly focused on Unit testing and did not bother much with writing any E2E UI/API tests

### What was good? 👍

- A dedicated automation team meant there was focussed attention on building frameworks and tools and automated test
  cases were authored
- Such a team helped onboard quality engineers and developers to test automation
- Solutions were really high quality since the team was outside the bounds/churn of the regular product release cycle
- API first focus meant we maximized value from test automation since the test suite was fast and reliable
- Using python language for everything meant it was easy to onboard new members since there was a great expertise

### What could have been better? 👎

- With timezone differences and very little overlap, collaborating with the existing developers and quality engineers
  based out of the US was challenging
- We missed signals on what features are being worked upon and automating which cases would add the most value to
  release velocity
- Devs still did not write Automated E2E tests thus leading to not making automated testing mainstream.

## Embedded QA + SDET and communities of practice

![](assets/images/2022/11/testing-setup-3-embedded-qa-and-sdet.png)

After a wonderful year and a half at Planview, I switched to Gojek Bangalore in 2018 and joined their Logistics team as
a Product Engineer - QA.

I joined a cross-functional team of Mobile, Backend devs, Designers, and PMs that were building consumer and
driver-facing mobile apps on Android and iOS platforms. My team had one contingent worker as QA from ThoughtWorks and
one QA in Jakarta

At the time, Gojek had a very low Full-time QA employee footprint and was using companies like Thoughtworks and
TestVagrant to augment the staff. TestVagrant was leading the building of common frameworks for the company across
Mobile, API, and Security domains as well as had embedded themselves into different teams to support testing.

In general, each team had the autonomy to build its own frameworks and while common solutions were available they were
not generalized enough for all the different teams.

I was playing the hybrid role of leading the QA effort by hands-on testing features, developing test plans, and also
building automation solutions, and mentoring other QA engineers in my team

I leveraged existing frameworks and build automation and tooling for my specific team's problem domain including writing
Java and Appium-based Android UI automated suite for the consumer app, Kotlin-based Backend API automated suite for
microservices, Load testing with Locust and Python, and multiple other utility scripts in Python to automate common
tasks.

I also mentored a couple of QA engineers from consulting groups and then later on a couple of FTE hires. Within a couple
of years, I was directly leading 2 SDETs. By the time I left, I was leading an 8-member quality engineering team with 3
Lead SDETs and their smaller team each owning a part of apps/backend for the logistics group. How that story unfolded is
probably a story for another time.

### Communities of practice

In the initial days, the QA leads from different groups used to meet frequently to share how they are solving
automation/testing problems in their teams and find the scope of using common solutions

Each team had its own priorities and was moving at its own pace. There was no central leadership and the QA in each team
used to report to either a Dev manager or a head of engineering leading to multiple reinventions of the wheel and a lack
of overall alignment on frameworks.

While engineers wanted to build frameworks for the Gojek scale, often they solved their specific use cases for their own
teams without caring much to generalize it for larger use cases.

Coupling this with having to test mobile apps for a Bi-weekly release cycle (called FCT or full cycle test) and
bandwidth to craft frameworks was a hard task.

Around 2020 end, Gojek hired a senior QA leader with proven expertise in building QA organizations, and that's when
things took a slightly different direction. I collaborated heavily with him to set up different communities of practice
each tackling a different part of the automation puzzle including Backend, Mobile, CI, Performance, and Community. Each
of these communities had its own dedicated leadership to drive those charters and align with engineers from multiple
teams.

I personally led the Backend automation community along with a couple of other leaders from different teams, we would
meet weekly and share knowledge and form a common roadmap of features and tools to build including Kafka automation,
test data generators, and standard libraries to test databases among many others. While other communities focussed on
mobile, performance, and CI tooling and built amazing solutions.

These solutions were designed keeping in mind the needs of all the automation teams within the Gojek scale and SDETs
from these different teams were members of these communities. Also, we presented these in engineering showcases and all
hands and even had dedicated ones just for QA. I remember different heads of engineering and even our CTO attended these
and was amazed by the number of features/capabilities the team was able to achieve within just a few months.

In hindsight, having a single-threaded leader and a better mandate to build common solutions really helped since it was
a rallying cry that was previously missing.

### What was good? 👍

- Collaboration between QA leads/team members was great since we could share our pains and also solutions
- QA embedded into product teams meant there was someone who knew those systems pretty well and could coach developers
  about good testing practices
- Later, having a mandate from the organization leader helped bring different teams together to build common solutions
  and avoid reinventing the wheel by 10 different teams
- Giving SDET/QA the autonomy to write their own automation makes sense since they would automate the higher-priority
  cases first
- Organizing different communities within the company so that engineers can learn and contribute to their interest areas
  builds a great learning culture

### What could have been better? 👎

- The community model meant there wasn’t a dedicated team building tooling/frameworks and keeping it healthy
- There was always a bandwidth crunch reported by community members since they were balancing their Product QA
  responsibilities (manual and automation) along with trying to build robust solutions for all
- Devs were not contributing to E2E automation. There was a pretty limited understanding of good unit/integration
  testing as well.

## An Automation Platform team

![](assets/images/2022/11/testing-setup-4-platform-team.png)

After close to 4 years at Gojek, I made a big career move and joined Meta in their London office within their Test
Automation group for WhatsApp. This group was responsible for building testing infrastructure and services for client
apps on Android, iOS, and web platforms

WhatsApp has a small team of experienced QA leaders who lead the testing efforts including creating and maintaining test
plans, helping deliver quality, and supporting product teams on a feature-by-feature basis. To ensure all the required
tests could be executed it uses Contingent workers from consulting companies.

Within WhatsApp there is a ruthless focus on Quality, It’s actually one of the core values of the company. Our director
created org-wide goals around code coverage and quality metrics and there are senior engineers from different product
teams that act as DRI (Directly responsible individuals) and act as seasoned Quality champions and help raise awareness
about Testing as well as keep track of testing efforts.

Here, Developers own writing of unit, integration, UI tests, and even some E2E tests using an Internal framework. This
setup is quite different from all other setups I had worked in so far.

I was in a team that enables developers to write these automated test cases by providing guidance, building framework
capabilities, and tooling, and raising awareness about software testing.

We also help devs by answering any questions about their tests such as helping them understand why the tests fail in the
way they do, and how to tackle flakiness. In general, this team was free to come up with their own roadmap aligning with
the organization's priorities and OKRs.

Multiple Testathons, Testing sprints are done, wherein devs focus on writing tests and thus improving code coverage and
further helping teams reach desired quality levels

With such a setup, there are literally thousands of automated test cases (unit and UI) written that execute for every
change in the app and even in multiple continuous runs providing timely signals to developers. In case a change (called
diff within Meta) fails, appropriate tasks are created for the owning teams on call and that brings high visibility to
any issues.

### Is this the perfect setup?

Yes and No, It certainly works quite well.

Our app has more than a billion users and we can boast of world-class reliability, privacy, and security rigor

Developers owning authoring of tests is a wonderful culture to have, this allows teams to move fast without being
bottlenecked on an individual to write tests for them, it has the caveat wherein some quick tests are written without as
much care as production code.

While devs are probably in the best position to write solid automated cases, the incentive to ship features and
deadlines means that sometimes corners are cut and poor quality automated tests are written that are often flaky.

Also, this means deep testing sometimes gets skipped since there are less no of dedicated testers on the team who
challenge the boundary of the system from every corner.

Having an automation platform team definitely is a big plus and I feel something that should be present in whatever
shape or form is possible. Automation engineering is a big space and needs dedicated bandwidth to keep the ship
well-oiled. In the absence of organizations, we risk automation becoming brittle and ultimately ignored.

### What was good? 👍

- QA leads coaching product teams and advising on testability, priority, and health of the app releases is good
- A dedicated platform team to build infrastructure, tooling, and frameworks mean these are well maintained and
  continuous improvements are made to DevX and improving quality
- Devs owning test authoring unburdens the QA team to focus on larger quality concerns and drives the effort

### What could have been better? 👎

- Quality of tests, Addressing flakiness are first-class concerns, if teams had some dedicated SDETs, it would mean Devs
  would get a helping hand, and the level of tribal knowledge around Test automation would also increase
- Having only a platform team risks the team building solutions in their own silos without being connected to product
  teams, having a community of practice would certainly help.

## So does a perfect setup exist? 🪂

Thanks for reading this pretty long write-up, hopefully, it was insightful. I’m not sure that a perfect setup really
exists anywhere and it's always a continuum. However, elements of these setups combined might work for your context.

Having a long career in testing affords you the wisdom to understand that strictly prescribing some solution without
understanding the problems and context would rarely be effective thus I think its a matter of putting our brains to it
and trying and experiment with some of these formats and see if you create value for your testing organizations.

## Over to you 🫵

What other testing organization setups have your observed? And what aspects about them work or do not work as per you?
Let’s chat in the comments.

## Before you go

Thanks for spending your time reading this post. 🙏

💡 If you found this insightful or helpful 👍🏼, then please take a few minutes and share it with your friends and
colleagues or on your social media accounts. Every share helps this grow and **"sharing is caring"** 🫂 isn't it?

Before you go 🙌🏼. Did you know?

- I publish a newsletter ✉️, **Subscribe** to 👉 [newsletter.automationhacks.io](https://newsletter.automationhacks.io/)
  to get this in your email inbox
- And, also recently started a YouTube channel 📺, **Subscribe** to 👉
  [automation hacks](https://www.youtube.com/channel/UC-KAka-3EgsbF1kekh_uYJw/featured) to not miss out when a new video
  is out.

I go deep into **Test Automation** and **Software Testing** in both these platforms as well and you may find subscribing
valuable to your learning journey

Have Questions 🤔 or Feedback 😉?

Please let me know in the comments (I promise I read them all ✌🏼) or you can ping me over Twitter or LinkedIn at
`@automationhacks`

Until next time, Happy Testing 🕵🏻 and Learning! 🌱
