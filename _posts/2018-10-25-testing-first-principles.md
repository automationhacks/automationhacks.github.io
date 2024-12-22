---
title: "Testing: First principles"
excerpt: "What are some of the first principles of testing that every tester/engineer should know of"
permalink: /2018/10/25/testing-first-principles/
categories:
  - "Software Testing"
  - "QA"
---

![Wikimedia Commons](/assets/images/wp-content/uploads/2018/10/39f67-0xev6ecbq4wvei1u4.jpg)

Hi there!

I have been working as a tester throughout my career and have always been and still am very
intrigued by the unique breed of individuals testers typically are. We are called by so many
different titles (QA, Quality engineer, tester, SDET… and so on) and we play so many different roles
within a products life cycle whether it being a coder, testing app from different layers, product
and systems thinker, agile coach etc.

Throughout this journey, I have observed some practices, aspects/qualities which in my experience
form the core of testing as a skill.

Well, in this blog post i wanted to share my thoughts on what are some of **_First principles_** in
testing which every new budding/experienced tester should definitely be aware of or follow in this
day to day life.

---

#### _Testing is almost always exploratory in&nbsp;nature._

This is probably the most important thing to grasp and at its heart, is the essence of testing. We
can come up with elaborate test plans and thousands of automated scripts/cases, but some of the best
scenarios and bugs in the app under test are usually identified when the tester is able to wear
different _thinking hats_ and **explore** the functionality from different contexts.

> Always be curious and never trust when a developer says something will “work” just fine and needs
> not to be tested **_🤔_**

#### Know your product and its customers

As a person working in quality, common expectation from us is to typically wear your customers shoes
and understand user journeys that they will take while using the product.

In this day and age, Understanding how customers are using the app and **_collection and analysis of
data_** to grasp what is of real value to the customer can be the difference between success vs
losing your customers to a competitor’s product. We should challenge ourselves to rise above just
**checking functionality** but rather to think about flows E2E from different perspectives to
eventually maximize the business impact.

#### Happy paths and test prioritization

Now this might be stating the obvious but one of the important goals to strive for is to ensure your
apps happy paths are **_never_ _broken_** in production and learn to **_prioritize_** the test cases
based on context in which you are testing. We need to be always have an intelligent suite of tests
which could be run to get fast feedback about the health of the app before pushing stuff off to
customers.

#### Bug hunter?

No app is perfect and there are always bugs to be found if you are curious enough to dig through
different layers of the stack (API, integration, network or database). Challenge yourself to
**really understand** how the systems you test work under the hood. What are the nuts and bolts and
most importantly areas where testing is not being done. 😎

#### Understand different aspects of&nbsp;testing

A testers ability to come up with great test cases are mostly proportional to the amount of
knowledge you have about the product and how critically the individual thinks. As a quality coach we
should know what different layers testing can be done.

Understanding how testing can be done at different levels like Functional (Blackbox, whitebox, UI,
API), Unit/Component tests, Integration, Non Functional (Security, Performance, Accessibility,
Compliance, Usability) automatically enhances your chances of designing a more robust test plan.

#### Automate the boring repetitive stuff

Well, lets admit it, no one likes to do the boring stuff. 🤷‍♂ Tests typically follow simple pattern
at its core like **_input, execute and assert._** Unless you are a 🤖, one would NOT like to repeat
the same cases on every new build that is churned in your CI (Continuous integration) pipelines.
Hence the dumb advice: **Automate the repetitive stuff and let machines do the stuff they are good
at.**

Focus more on exploring unknowns in your app and using your creativity or thinking out of the box is
what ultimately adds most value to a product.

#### Don’t automate everything

Most managers and product stakeholders like to chase the ever elusive metric of 100 % automation,
However i urge you. **_Don’t fall into this trap._** Automate areas where maximum value can be
derived. As an example try to cover most functional behaviors through API tests instead of having an
endless battery of failing UI tests.

#### Write Good documenting test&nbsp;cases

Just like cleaning code is important to ensure you don’t leave a mess behind for the person who
comes after you. As a tester it is quite important to ensure you tests remain relevant and
meaningful.

#### Shift left

Shift left and try to be part of entire SDLC, you would be surprised how many times you as a tester
can catch gaps in requirements analysis and help developers deliver a much more quality product by
being involved early in the process.

#### Learn to&nbsp;code

Learn to code in at least a static and dynamic language. Learn the craft of programming and
refactoring. Not only would you be able to automate stuff. This can potentially even help you to
shift in a grey box test role where you can understand gaps with dev code commits. Plus the most
important reason for this is. **_It’s way more fun…_ 😉**

---

That’s it folks.

What do you think of the above? Do you have more thoughts to add? Let me know in the comments
section below and if you found this useful why not share it with a friend or colleague.

Until next time.
