---
title: Why automate tests early
excerpt: A post on why test automation early and in parallel to the development cycle can help you scale faster and give better and quickly repeatable confidence over your feature ship. And why is there even a need for this in the first place?
permalink: /2020/03/21/why-automate-tests-early/
image: /assets/images/wp-content/uploads/2020/03/chris-liverani-hujdz6cjeam-unsplash.jpg
categories:
  - Testing
  - "Test automation"
---
A post on why test automation early and in parallel to the development cycle can help you scale faster and give better and quickly repeatable confidence over your feature ship. And why is there even a need for this in the first place?

![](/assets/images/wp-content/uploads/2020/03/chris-liverani-hujdz6cjeam-unsplash.jpg)

Photo by&nbsp;[Chris Liverani](https://unsplash.com/@chrisliverani?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)&nbsp;on&nbsp;[Unsplash](https://unsplash.com/s/photos/fast?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

As a lone tester/SET (Software engineer in test) working on an agile team, the core activities to be performed are test planning, design, and execution (among many [others](http://automationhacks.blog/2020/02/29/the-problem-with-titles-for-testers/)),

Notice when I mention these phases, I am not calling out **manual vs automation** since these **should** actually go hand in hand and are part of the same whole.

In an uncertain product development environment often things move fast and features/spec changes as more folks (product, design, sales, business, devs) get involved in the process and there is _almost always a hard deadline_ _to chase_ and an **apparent** shortage of time to ship.

## Let's not automate till the feature is <span style="text-decoration:underline;">well tested</span> and <span style="text-decoration:underline;">stable</span>

One of the classic arguments on why to **NOT** automate tests **early** in such an environment is that:

  * It's _way_ easier to write and modify these test cases in a test management tool manually as the specs change around us and adjust to these changes or worst still, let's not write any tests for now and use spreadsheets or docs to track.
  * You might also say, that since the specs are not completely frozen, any automation code that I may write <span style="text-decoration:underline;"><em>might</em></span> get thrown away at the end of the day.
  * Developing the basic framework code to enable writing these tests or the actual tests will take a lot of time which we don't have now.
  * We will be stuck with maintenance early on before the feature is really baked.

Fair enough.

While all these are valid concerns on their own right and do reflect a certain reality on the ground. However, let's not give up on automation _just yet.&nbsp;_😉

## The problem with just manual testing

Cases developed and tested manually in an exploratory fashion are definitely flexible and powerful. Any coded test would not be able to shift dynamically in all the available paths.

However, there are some caveats to skipping automation completely in this phase.

Consider this common scenario:

<blockquote class="wp-block-quote">
  <p>
    Developer: Oh, I have made some <strong>more modifications</strong> to the code based on the spec change or the bug which we found earlier, Can you please test this again?
  </p>
</blockquote>

Yes, I know what you as a tester are thinking 😞

<blockquote class="wp-block-quote">
  <p>
    Tester: Did I just <strong>waste</strong> spending all this time checking this build against a moving target?, o_O Well can't do much now since the feature has to ship fast,
  </p>
  
  <p>
    Let me repeat <em>some</em> of these cases considering the less time that i have to test to see if something is broken
  </p>
</blockquote>

While you might discover a new bug in this new code, often times the real killer is regression bugs. Areas in the app which you have already tested and might have grown slightly bored testing of as well.

Your biases play against you and you might not want to repeat the whole effort from scratch again and might skip some areas believing that they don't have any bugs.

The consequence.

<blockquote class="wp-block-quote">
  <p>
    Regression bugs slippage into later phases of software development which we all know as more expensive to fix. Multiple status calls with stakeholders and bargaining for more time.
  </p>
</blockquote>

Does the above seem familiar? I am speaking from experience and have faced this situation some times and let me tell you this scenario keeps on repeating again and again in sometimes nefarious no of loops.

Yes, multiple cycles of testing do highlight many of these issues early. But it still leads to another problem.

## Catching up with automation

Let's occupy the most optimistic viewpoint and _assume_ this feature does go live with fewer issues and you **now start automating** these cases which are supposedly stable.

We still land into another problem.

Developers, PM and the business <span style="text-decoration:underline;"><em>will not wait</em></span> for you to finish the automation before they pick up the next feature/project in the backlog.

This whole story that we just walked through might get started from the beginning again and in the end, you are left with a huge mess of backlog items to automate with the additional problem of seeking context for the earlier features, while juggling the testing activities for the new feature.

<blockquote class="wp-block-quote">
  <p>
    🙁
  </p>
</blockquote>

## So what is the solution?

Let's take a step back and think through (_retrospect_) on what could we as testers do differently.

## Estimate and plan well

The first obvious thing to do is to ensure that the time estimate for testing and automation is part of the estimate for a features timeline and overcommunicate if needed.

While the devs are writing the code to develop a feature, You can author initial test cases as a high-level plan as preparation and encourage devs to do initial testing well enough to ensure fewer chances of slippage of obvious bugs and to build testability from the start.

Use all available resources at hand to come up with a good test plan:

  * Use the features spec doc
  * Talk to the product managers and business team to understand the implications of the feature
  * Identify what areas pose the most risk
  * Identify the priority of cases to test first
  * Do not bother to write all the cases at this stage, you will come to understand the feature better when you test and would be able to add more detail.
  * Ensure all the major cases and risk areas are identified. Get these cases reviewed by dev and PM to ensure you are not missing anything.

## Be part of code review

  * Once the coding is done, ensure you take a look at the checked-in code in the merge request and ask probing questions on the test coverage
  * Suggest any missing cases that could be covered at a lower level (Unit/Integration level) for the devs to add and most importantly _ensure they get added._

<blockquote class="wp-block-quote">
  <p>
    A Tester needs to act as a quality coach and nurture and probe devs into donning the testers hat and build/add releavant tests.
  </p>
</blockquote>

## Automate API cases first

We all know that developing UI automation cases for web or mobile is a challenging task and sometimes an exercise in frustration as you have figure out:

  * If appropriate identifiers are built-in
  * Figure out an appropriate wait strategy
  * Run the cases multiple times to ensure that they are reliable.
  * Additionally, cross-browser or mobile device fragmentation is also a concern

Developing stable automation in the appropriate timeline might not always be realistic.

By contrast, If a feature involves interaction with an API.

### The benefits of automating down the stack

Then it is much easier and feasible to add automated cases since these typically involve doing an appropriate setup, action, and verification.

These cases do not involve any of the complexity of a UI while still giving you appropriate coverage over the functional flow of the application.

You can quickly prototype the APIs in postman and then write an API test for the same. Its easier to even run them in parallel further reducing the execution time.

It's a no brainer that any such cases should be automated first. Again do not bother covering all cases but target the cases which can mitigate the maximum risk and have higher priority.

## Automation high priority UI cases

If you do the previous step diligently, then what you would observe is that you have already covered most of the functional flow via API cases.

Now is the time to cover the cases which you can _only verify_ via the UI, namely can the user execute its user journey steps and perform the important actions.

You can use any of the UI automation frameworks for the same. Choose something that is easy to work with and add cases in and which does not give maintenance overheads later on.

<blockquote class="wp-block-quote">
  <p>
    <strong>Visual testing</strong> could help you add robust validations in a short amount of time without writing too many functional assertions.
  </p>
</blockquote>

## All cases should run in CI from the start

An important heuristic is to ensure you have a basic framework in place to add new components and tests in. That implies having a stable CI set up to run the cases in (either a VM, docker container, etc) as well as a reporting framework to analyze or debug any failures.

## So are all the problems solved?

This way, when the devs ask you to give an idea of whether we are good to ship, the only thing left is to run the automated cases and verify results

The more you follow approaches of automating early, the better the amount of regression coverage you can quickly ascertain.

Machines are very good at following instructions and they do not tire. While the automated tests do their job, you **are freed up** to do exploratory testing activities to figure out those hard to find edge cases while resting assured that all the major functional flows are working fine.

Surely this can be an improvement over the initial scenario, however, let's not forget that automation is hard work and stable and fast automation is an even uphill task.

There would be a requirement to modify this automation as features change or specs are modified and there could be maintenance requirements in case of test failures.

If you are a single tester on an agile team then the only real option you have at success is to ensure **more bandwidth&nbsp;**and some ways of doing that are:

  * Bring in developers to also write some of this functional automation,_ For this purpose, it's a good idea to have **your tests as part of the dev repo if possible** in order to reduce the barriers to contribution.
  * Augment a couple of dedicated testers to share this load and ensure the team can deliver on time.

## Conclusion:

To conclude, automating early has lots of benefits and is an ideal to strive for in your team. This is not an easy path and requires a mindset shift for many people but can surely add a lot of agility and better quality culture in the team.

This approach does work well for some teams but might not always work in all contexts. As always you as the tester understands your product and team the best and can tailor these to meet your specific context. However, if you strive to achieve this ideal then your life as a test engineer would surely be way better than always playing catch up.

What do you think? Do you have any other thoughts or insights? Share them in the comments and I would be very happy to learn from them. Until next time. Cheers.