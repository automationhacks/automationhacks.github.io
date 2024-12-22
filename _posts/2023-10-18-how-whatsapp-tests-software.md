---
title: "How WhatsApp tests software?"
excerpt: "How do engineering teams at Meta enable Quality for an app with a 2B+ monthly active users"
permalink: 2023-10-18-how-whatsapp-tests-software
published: true
image: /assets/images/2023/10/key-components-for-delightful-test-automation.png
canonical_url: "https://newsletter.automationhacks.io/p/how-whatsapp-tests-software"
categories:
  - "Meta Engineering culture"
tags:
  - "Meta"
  - "WhatsApp"
  - "Software Engineering"
---

<figure class="image">
    <img src="assets/images/2023/10/key-components-for-delightful-test-automation.png" alt="Image showing few blocks with key components towards test automation">
</figure>

I was reflecting on how the WhatsApp team (WA) tests its apps and what other teams across the globe can learn from their test engineering practices. This is also a recurring question that I get from many people, So let’s shed some light on this, shall we?

## Testing approach

I was a member of the WhatsApp Test Automation team in their London office for one and a half years between the end of 2021 and close to mid-2023 and I had the privilege to take an up close and personal look at how an app with 2B+ users is tested.

The WhatsApp Test Automation team was responsible for developing test infrastructure, tools, and frameworks to allow developers to write efficient tests for WhatsApp clients (notably Android, iOS, web, and desktop apps). It was a critical part of the testing strategy for the entire organization.

In some ways, the approaches are similar to any other consumer-facing mobile app with all the usual layers of the test pyramid. WhatsApp teams prefer to use many open-source tools to write their automated tests but also use many internal Meta tools and Infrastructure to supercharge their entire testing strategy. The testing approach for WA differs from meta apps quite significantly as well.

In this blog, I'll talk about two key aspects that enabled this strong culture of automation

- Frameworks and Infrastructure
- Teams and personas that enable this

Let’s dive in 🏊

## Test Frameworks

Let’s first look at the different layers of the test pyramid and see what are the different tools and frameworks being used.

For mobile frameworks, Automated tests were written at all the layers of the test pyramid with a high no of espresso and XCUITests and a comparatively lower no of E2E tests.

### Android

- Unit tests: [JUnit](https://junit.org/junit5/), [Roboelectric](https://robolectric.org/)
- UI tests: [Espresso](https://developer.android.com/training/testing/espresso)
- Screenshot tests: [Screenshot tests for](https://github.com/facebook/screenshot-tests-for-android)Android ([read more about this here 🔗](https://facebook.github.io/screenshot-tests-for-android/))
- E2E tests: [Jest-based](https://jestjs.io/) internal E2E testing framework

### iOS

- Unit tests: [XCTest](https://developer.apple.com/documentation/xctest)
- UI tests: XCUI Tests
- Snapshot tests: Probably similar to [GitHub - uber/ios-snapshot-test-case: Snapshot view unit tests for iOS](https://github.com/uber/ios-snapshot-test-case/)
- E2E tests: [Jest-based](https://jestjs.io/) internal E2E testing framework

## Test Infrastructure

WhatsApp relied on a lot of Internal meta infrastructure for its device testing and CI needs.

### Code coverage

- Internal infra to collect unit and UI tests code coverage
- Internal dashboards to visually trend and metrics around code coverage

### Version control

- [Git](https://git-scm.com/)
- [Mercurial](https://www.mercurial-scm.org/)

### Test runner

- Internal test runner

### Devices and emulator

- Internal system

### Build

- Android: [Gradle](https://gradle.org/), iOS: [Xcode](https://developer.apple.com/documentation/xcode/build-system)
- [Buck2](https://github.com/facebook/buck2)

### Test Reporting

- Internal logging infrastructure
- Test monitoring in [scuba](https://research.facebook.com/publications/scuba-diving-into-data-at-facebook/)
- Internal reporting infrastructure

### CI

- Internal CI (read a [blog about it here](https://engineering.fb.com/2017/08/31/web/rapid-release-at-massive-scale/))

### Testing services

- [Test selection](https://engineering.fb.com/2018/11/21/developer-tools/predictive-test-selection/)
- Test recommendation
- Monkey testing with [Sapienz](https://engineering.fb.com/2018/05/02/developer-tools/sapienz-intelligent-automated-software-testing-at-scale/)
- Static analysis with [Infer](https://github.com/facebook/infer)

  As I collected this list, I realized Meta (formerly Facebook) is a company with an awesome engineering culture and they publish blogs about a lot of their internal tools to open sources and talk about it. If you want to get other ideas on their testing approaches, I suggest following [DevInfra blogs](https://engineering.fb.com/category/developer-tools/) and checking out the GitHub[project](https://github.com/facebook)s for further insights into how to maybe adopt some of these in your own teams.

## A buffet of tools/frameworks 🧑‍🍳

It's quite fascinating to see that there is such a rich set of tools and frameworks all supported by scalable infrastructure. Engineers thus spend less time maintaining this or fighting the infra and rather focus on writing their tests knowing fully well that it would run and scale as long as they write tests by following recommended practices.

You may have also noticed that most of these tools are used in many companies and startups and there are open-source solutions available to address these problems as well.

It’s just that at Meta the internal tools are heavily optimized through the virtue of significant engineering time over the years and integrate quite well with each other to create an ecosystem. It’s also a slight learning curve to understand all of this and the Test automation Infra team had the privilege to be right in the middle of it all.

## So, How does WhatsApp “really” test its software?

![Test avengers assembled](assets/images/2023/10/test-avengers-assembled.png)

At this point, you might be thinking, hmm, so WhatsApp uses a bunch of tools to enable automated testing, and may be wondering how these different teams and engineers are organized.

Let’s look at the testing setups and the major personas involved.

### Engineers own writing automated tests

At WhatsApp, developers write the bulk of the automated tests themselves.

They write app code, along with unit and UI tests and occasionally some E2E tests as well. I had previously written a short note on this cultural practice, feel free to read about it [here](https://automationhacks.io/2023-07-09-meta-engineering-practices-engineers-write-tests).

Here, I’m primarily referring to mobile engineers since WhatsApp being a chat app is very client-heavy. There are server teams that follow similar philosophies and write their tests themselves.

In some respects, this is quite nice, since engineers are responsible for their tests and also for any SEVs (production incidents), they are naturally motivated to write appropriate levels of automated tests to cover their code and mitigate any risks.

I did not see any dedicated automation team of SDET/SET (Software engineer in tests) staffed in feature teams to take up writing automated tests which are otherwise quite common in start-ups and many other companies.

Some natural questions arise on this practice:

- What are the 1st and 2nd order impacts of such an approach?
- And what about tooling and infra. Someone needs to maintain all that right?
- Are tests written by engineers of higher quality compared to being written by dedicated testing specialists?

Well, You are right on the money to question this.

#### Pros 👍

- One of the benefits of this is that in general a lot of automated tests get written.
  - If they are of bad quality (i.e. flaky and unreliable) then the infra itself takes care to remove them from running executions and notifies the author via a task system.
- Another benefit is that there is no bottleneck on a dedicated QA team to write all the automated tests
- Engineers don’t worry about building tools and infra and just make use of existing stuff to author tests
- Flaky tests get fixed faster (since more engineers are looking at that)
- Engineers understand testing practices better and in this case “Quality is everybody’s responsibility” translates to something meaningful rather than posters on a wall

#### Cons 👎

- Tests sometimes do not have robust assertions
- Tests have a lot of duplicated code without much care of putting up the right abstractions. Since engineers view writing a test as just another task on their checklist to ship a feature, they do not pay huge attention to building good reusable abstractions
- A lot of flaky and broken tests are written

### Infra teams build tools and frameworks for testing

At WhatsApp, multiple Infra teams are responsible for just that.

Their charter involves thinking about testing strategy holistically, both in-depth and in breadth. These teams do not write tests. But they help build sufficient levels of test infra and tools to support developers writing their tests.

They also worry and care about the quality of the app deeply and build solutions to make life easier for developers. They are seen as Test Automation champions and experts whom dev teams rely upon for guidance and for building any specialized solutions for their specific needs. They also build educational materials like internal docs and courses on Test automation.

The need to have this dedicated group of individuals is super clear from my viewpoint.

Why?

Glad you asked. 😉

A developer tasked with feature work and automated testing will barely have time to build systematic solutions to testing problems that scale well. An Infra dev does not worry about writing tests or day-to-day feature delivery and can solely focus on building tools (regardless of the testing fidelity it targets). Since they build tools for not just one team, it also leads to better and more generic solutions that can be widely applicable.

The key sauce is a leadership team that supports and sees value in this to secure buy-in and funding. Without that, such a team cannot prosper and at WhatsApp, we were fortunate to have very strong leaders behind this team.

### Prod Ops team support infra teams

Now while Infra devs are solid software engineers, some having prior backgrounds in being full-time mobile and backend software developers, they very occasionally come from pure testing backgrounds (QA or SDET).

They know how to build infra and tooling solutions but don’t have deep connections with feature teams to understand all the nitty gritty of SDLC or spend a lot of time playing with different test frameworks and approaches.

The Prod Ops team is a team that filled this particular gap. It was staffed with engineers called **TQS (Technical Quality Specialists)**

This team is in some ways similar to a traditional QA team responsible for leading the quality charter across the product. There are a few Android/iOS developers in this group as well.

They are responsible for a bunch of important activities.

- They are experts in exploratory testing and understand the product and flow deeply. They would focus on the big bets for the product and ensure all the right things happen in terms of testing and quality, think of features like channels, avatars, etc.
- They support Infra and feature teams by:
  - Doing Test design and suggesting test cases, prioritizing them in terms of value
  - Ensuring healthy test suites by removing redundant cases
  - Supporting production testing and experimentation
  - Triaging Customer issues and bringing feedback to product and leading bug triages
  - Building insightful dashboards into the state of quality
  - They sometimes author automated E2E tests as well and help with test flakiness analysis

They are a valued and core team with complementary skills that enable WhatsApp's culture of quality and in my opinion, an essential glue that ties the whole thing together and enables this setup to work well. This team also has strong leadership support for its charter.

### Embedded Test leads within Feature teams

In addition to these, WhatsApp designated an engineer from each feature team as a Test lead role who was responsible for reviewing the test plan for the current quarter, coming up with areas that lacked coverage, and rallying their developers to write tests for those.

They would also be in sync with the Test automation team to develop know-how of current tools and features under development and help drive awareness to them within their own teams.

There was a regular meeting setup where the Test lead would present their plans, gather feedback, and then go back and help drive the execution. The whole project was managed by a Leadership SWE within WhatsApp.

In my opinion, generating such thought leadership within Teams was a catalyst in ensuring WhatsApp's commitment to quality was upheld and very stable releases went out.

## Conclusion

To summarize:

- WhatsApp makes use of automated tests to drive quality and test coverage
- WhatsApp engineers write their own tests
- The test automation team helps build Infra and tools to support engineers
- Prod Ops QA supports Infra and feature teams by leading the quality charter
- Dedicated thought leadership around Test engineering by developers helps drive this
- Strong leadership support towards these teams, and staffing them with talented and senior engineers helps in moving the needle in the right direction

Did you notice how all these teams and functions work towards the common goal of shipping high-quality code faster? Test automation and Quality are gigantic spaces and require a lot of nuance and skills to ensure the right strategic bets make their way into the development workflows.

In summary, it does not take a few individuals but a whole village to care about Quality and investment from leadership in enabling such setups.

Hope this was helpful. Let me know in the comments if you have thoughts or any questions about this.

Thanks for the time you spent reading this 🙌. If you found this post helpful, please share it with your friends and follow me (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time, Happy Testing 🕵🏻 and Learning! 🌱 | [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
