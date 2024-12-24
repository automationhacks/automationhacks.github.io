---
title: Simple truths of Software Testing and Automation
excerpt:
  "Software testing and Test automation is nuanced field. There are many common sense truths that
  engineers should take care. This post elaborates on a twitter thread an the same topic"
permalink: /2021/06/23/simple-truths-of-software-testing-and-automation
image: /assets/images/2021/06/undraw_people_search.png
categories:
  - "Software Testing"
tags:
  - "Career growth"
---

<figure class="image">
  <img src="/assets/images/2021/06/undraw_people_search.png" alt="Lady searching with a microscope">
  <figcaption>Source: Undraw by Katerina Limpitsouni</figcaption>
</figure>

Sometime back, I started a twitter thread, capturing some musings about Software testing and test
automation.

Most of these were **boring**, **common sense** facts about Software testing practices and have been
spoken or blogged about heavily. For me, It was fun to do a mind dump of these **mental models** as
the act of writing stuff down really helps me crystallize ideas for myself

Some people liked this thread asked if there was a blog post about this somewhere. Sadly there was
none at that time.

Hence the reason for this blog. So here we go.

Let's do this. 💪

I'll post each tweet and explain or give some additional context about them. Hopefully you'll find
them useful.

> Disclaimer: As an experienced engineer these might be really obvious to you. But a refresher has
> never hurt anyone has it? 🤷

## 1. Early involvement

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Simple things we know to be true about Software testing and automation but often forget.<br><br>1. Involve testers right from the start of a feature and involve in the design process to get valuable feedback and better refined acceptance criterion's</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339944159658930179?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Really good Testers possess lots of **business context**, when you involve them early in the design
process, they can help spot gaps in your specs, **missed corner/edge cases** and **Consumer**
perspective. You as a PM/Dev Lead can capture all these very early in the process.

In the end the product is better off and this also helps reduce late spec missed during actual
testing phase, at which point its very expensive to redo design to accommodate flows that were not
initially considered

> 💡 Testers: If you find yourself being left out because, "Well, Dev's and PM's are busy in the
> design process", Don't sulk, raise your hand up and self invite yourself, doing enough of this
> shows you are willing to be a stakeholder and take ownership and in most cases, you'll be included
> right away. Makes sense?

## 2. Shift left

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">2. Shift quality and automation left, that means Dev&#39;s also write automated tests, testers look into design and UX much early and even start laying foundation for automation much early.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339944564006604800?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

We spoke about early involvement in Tweet # 1

With automated tests, Why should testers have all the fun? 🤷

If you believe in QA as being the gatekeeper and only person responsible for quality/automation,
please read on a related post: [Testers are not the last line of
defence]({% link _posts/2019-06-24-testers-are-not-the-last-line-of-defence.md %})

Testing is a team sport, and dev and test are really two sides of the same coin

Devs should also be comfortable with the **automation code** and be able to add new coverage or
modify existing cases as needed. Most Developers that I know of, are more than happy in helping out,
You as the tester just need to help them out with the required context

Another side benefit of this is that Testers get **more bandwidth** to create robust automation.

Win. Win. 🙌

## 3. Don't run automated cases manually

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">3. Don&#39;t repeat manually what is already automated, it doesn&#39;t make any sense. Use the time to test different things and unexplored areas</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339944746135900163?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Some exploratory testers lack confidence in automation, and are skeptical if the automated test will
cover everything? They would often repeat the same cases by hand.

It's a fair question, but can be easily answered if the said Tester can grok the automation codebase
and find if the required assertions are in place.

To me, repeating cases by hand is just wasted effort and diminishes the value proposition of
automation. We should strive to build **robust automation** and use the freed up time to test
different aspects of our system.

## 4. Build automation early

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">4. Cost of test automation is amortized with every CI run, build more automation and early. You&#39;ll get more breathing space plus machines are damn good at these repetitive tasks</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945076433199105?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I wrote about this in an earlier post, but you should strive to write some automation early and put
it in your CI system, this way you can very quickly run this suite to gain confidence about your
system.

Nobody likes to run same cases every hour for every new dev build is it?

Its much better to automate these and get them off your plate. Interested in reading more about
this? [ Read: Why you should automate tests
early]({% link _posts/2020-03-21-why-automate-tests-early.md %})

## 5. Exploratory over scripted tests

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">5. Use manual testing for areas which really need it, accessibility, privacy, really hard to find bugs in untested corners, let your exploratory testers do what they do best, well explore the system. Don&#39;t make them execute repeated test scripts</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945343153160194?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Manual exploratory testing is really valuable, it involves someone using their **mind, creativity**,
prior **context** about the product to explore, break down the product from different angles and
often finds very hard to discover bugs.

However, If you ask your testers to run the same scripted tests in every cycle, Do you think, they
will take the uncommon sad path?

In most cases, the answer would be no, Not our of lack of interest but because they won't have
enough time

so we should rather automate these predictable cases and unleash our testers to explore the product.

> Note: Exploratory testing is not random testing with no aim, it is well structured and involves
> use of well defined **tours or charters** to cover a meaningful subset of the product. You can
> read more about it in amazing books like
> [Explore it! by Elisabeth Hendrickson](https://www.goodreads.com/book/show/15980494-explore-it)
> or
> [Exploratory software testing by James Whittaker](https://www.amazon.in/Exploratory-Software-Testing-Tricks-Techniques/dp/0321636414)

## 6. Automate the boring stuff

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">6. Please automate the boring repetitive stuff</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945442142916609?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Quite obvious,

- Don't repeat same `n` cases manually in a loop, rather automate them.
- Do you have to create some test data manually again and again, write an automated script
- Does some test take a lot of time and is painful to repeat, well you know what to do 😉

> If its boring and repetitive and does not require human intuition, automate it please 🙏

## 7. Start small and Iterate

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">7. For your frameworks, Please start small and iterate. Keep it simple and don&#39;t do a big design upfront. To enough to get a good picture and get started but don&#39;t write a thesis.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945758229860357?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I've learned from experience that doing **Big design upfront (`BDUF`)**, Writing really long
documents often, does not lead to good frameworks or tests.

Obviously this might not hold true in every single context, but its better to start small and then
quickly iterate. If you have to fail, you'll fail early and discover problems early as well.

Remember refactoring is your friend here. 🤝

This does not mean you throw all design docs out of the window, Do enough design to form a high
level idea, maybe a block diagram or two but don't really go deep into each component at this stage.

Let the code surface low level implementation details and then pivot appropriately.

## 8. Respect test pyramid

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">8. Write unit tests, check the integration points/contracts, Test your API endpoints, with a little bit of UI automation on top.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945945220280320?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

We are just describing the classic Test pyramid. Its a darn good idea to write the appropriate test
at the required level.

And yes, you as a Test automation engineer should go deep into the product stack and understand how
to write these tests. Don't wait for permission and Don't limit yourselves to writing only
Functional E2E tests.

If you want to know more about this, read
[Test pyramid](https://martinfowler.com/bliki/TestPyramid.html),
[The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) at Mr
Martin fowlers website

## 9. Write atomic tests

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">9. Don&#39;t write long tests. They will be anyways be flaky</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339946031555858432?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I don't think this needs explanation, As a rule of thumb Don't write tests longer than 10 Lines of
code. Even that is long in most contexts.

Write small tests that do one thing and assert its outcomes, your automated suite would really thank
you later since debugging would be a delight and these will run fast as well.

## 10. Build parallelization from the start

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">10. Design automation with tests concurrency in mind</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339946135868252160?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

While building a framework as soon as you have 5 sequential tests, Spend some time and make them run
in parallel. You can leverage capabilities in your test runners to do this easily

It can be a bit of work initially but the payoffs really are huge.

You'll observe them when your suite scales from 10, 100, 1000, 10000 tests. If you want to
understand Java concurrency a bit more read
[this post on MIT OCW (MIT Open courseware)](https://web.mit.edu/6.005/www/fa15/classes/19-concurrency/)

## 11. Design smart coverage

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">11. You don&#39;t need to test everything in all possible ways, just enough coverage to increase confidence in your releases.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339946330387431424?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This one is subtle, I'm sure you realize by now that every single test that you'll add to your suite
has a **maintenance overhead**.

To me this analogy seems reasonable, Imagine you are the gardener, You should treat your automated
suite or tests like a garden and regularly prune them to remove any redundant unnecessary tests.

Usually writing very targeted tests that business cares most about is the smart thing to do. Ask
yourself, can I write `n` smart tests that give me lot of coverage and confidence to release
features early. If yes, those are the ones you should write first.

## 12. Test sad path more often

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">12. We mostly test happy path so much, but ignore the sad path. Test that more.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339946482284126219?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Most testers are so often busy ensuring happy path works, and they never get time to test much of
sad paths.

What often gets ignored are the corner cases, on that unique Test/OS/screen size that often cause
lot of customer angst.

And, that's really really sad! 😲

Please test that more, write automation for happy paths so you get time.

## 13. Write hermetically sealed tests that detect changes

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">13. Tests should be small, focussed on testing one thing only, and isolated from each other, in order to be easily parallelizable and be deterministic. If the test fails, it should detect a change in the system.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1340208018311446530?ref_src=twsrc%5Etfw">December 19, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

We already spoke about this in Tweet # 9 and 10, however let me add few more aspects that classify
well written tests,

- Never ever write tests that share some common data, because they inherently force you into a
  sequential suite and we don't want that, do we?

Also Take your time and write **good assertion messages**, when your test assertion fail, and trust
me, they will, you should have a friendly message that explains where exactly it went wrong.

Its one of the most important things to get right but often ignored, please spend time on this
simple habit and trust me, the rewards would be immense

Needless to say, when you tests fail, make sure someone analyzes and reports it to appropriate
developer to get it fixed.

## 14. Keep your suites healthy

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">14. Continuously failing tests just leads to product teams ignoring the tests. Value of automated tests goes down drastically at that point. Fix any flakiness, raise bugs if the test fails.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1340208614464577536?ref_src=twsrc%5Etfw">December 19, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Automated tests are **not magic**, we often say, this suite is so flaky, it keeps on failing all the
time.

> Remember: If this keeps on happening, you have failed in your automation efforts.

Be afraid, be very very afraid of this!

Don't write new tests to show some coverage increase metric to management rather always keep your
existing suite green

Every failing tests is an opportunity to explore what exactly went wrong. You either find a product
bug, a problem in your test environment or a problem with your test itself. Use this opportunity to
design a better test, and please don't just re-run the test and ignore it saying it sure passed now.

## 15. Before automating, test it manually

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">15. To automate something, you have to test it by hand first, to understand how it works, its nuts and bolts, its failure points and then &quot;choose&quot; what makes sense and adds value before going ahead. Don&#39;t be in a rush to code. Think twice code once. 😉</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1340489072121298946?ref_src=twsrc%5Etfw">December 20, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Here is a silly phenomenon, we harp on automated tests as the promised savior.

It sure is fun to churn out code like a machine and automate **5 - 10** new cases per day to show an
upward trending graph. Management really appreciates such an SDET right?

However, if you are doing this activity for the praises and accolades, you are digging yourself a
**slow deep** hole.

In most cases automation for the numbers game is not really effective automation and we all fall
into this trap in our careers

Rather, I propose and encourage you to understand the full context behind the feature you want to
automate first and test it out once or twice by hand.

Some questions you can ask yourself:

- Is there any **value** in automating this?
- Is this better off being tested manually?
- Do I understand this feature enough?
- What sort of assertions should this test have?
- Should I break this down into multiple smaller tests?

This would ensure that when you get down to writing the automation, you already have a good mental
model about the feature and can write better tests.

> Also, don't forget to write documentation to help the next engineer who looks at this feature.

## 16. One size doesn't fit all

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">16. The approach that worked in one project might not in another project/org. Keep an open mind. Evaluate couple of automation tools before deciding on the best one for your specific needs and context. <br><br>&quot;If all you have is a hammer every thing looks like a nail&quot;</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1340490128880357378?ref_src=twsrc%5Etfw">December 20, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This has to be the most common mistake Test Automation engineer make, Tell me if the below seems
familiar?

A new SDET joins your team, after looking at the codebase they say, this code is very badly written,
we need to rewrite this and build something from scratch.

Oh no 😱, Really? Yet another rewrite?

Quite often, The **"shiny new framework"** is a copy pasted dump of code from their last company
codebase without comprehending or understanding if it really fits the need of the current team or
company.

Or someone has a favorite language and for some bizarre reason wants to write everything in Java
when you have ruby devs all over the company

Please stop 🛑, before you shoot yourself in the foot.

Every team, project, company is different. Joining a new team is wonderful since you can start a
fresh. Take time and understand all the context before you jump in and start making suggestions.

Quite often, you'll learn a lot more this way and also the changes you make would be constructive
and not destructive in nature ☮️🍃

And, you are not alone if you've made this mistake. I've personally made this as well and learned
from this. 😉

## 17. Asking right questions at the right time

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">17. Good testing is often asking the right questions, to the right persons at the right time!</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1350289376287154176?ref_src=twsrc%5Etfw">January 16, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The next time you have a project kick off meeting, don't just sit there idly with your camera turned
off and read something else or write yet another automated test.

Take an active role in the meeting, ask really good questions, this way you can ensure lot of good
testing happens before even a single line of code is written. Use this oppurtunity

## 18. Pair with devs more often

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">18. 3 ways to get developers to test more and better:<br><br>- Sharing: Share your AUT knowledge and tools<br>- Pairing: Ask what have you already tested? What&#39;s remaining? What is worrying you?<br>- Caring: Coach them with care.<br><br>Taken from <a href="https://twitter.com/alanpage?ref_src=twsrc%5Etfw">@alanpage</a> <a href="https://twitter.com/hashtag/testflix?src=hash&amp;ref_src=twsrc%5Etfw">#testflix</a> talk<a href="https://t.co/FTkjtp7wer">https://t.co/FTkjtp7wer</a></p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1365300798398156800?ref_src=twsrc%5Etfw">February 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I think [Alan page](https://www.moderntesting.org/) described this quite well and I'll recommend you
to check out his [talk on TestFlix](https://www.youtube.com/watch?v=fwD_ThSyTQk) on how to encourage
devs to test more and often.

In short, pairing with devs is going to be one of the **most valuable skill** you'll ever learn as a
test automation engineer. Do more of it!

## 19. Don't Trust "It will work, you only need to test this and that"

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">19. If the dev says: &quot;You don&#39;t need to test &quot;x&quot; aspect of the app. Is should work fine&quot; <br><br>Confirm this assumption and do test around to discover regression impacts. More often than not, You&#39;ll be surprised to know cases that were not considered.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1365310305446756354?ref_src=twsrc%5Etfw">February 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

If you hear your devs suggest this, please ask them why they think this way and have they regression
tested already?

Make sure you regression test every feature and never be satisfied with just testing the one change
that was made. It can be tedious but understand that often code breaks in other integrations rather
than the component that was changed directly

## 20. Pair some more

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">20. Don&#39;t expect Dev&#39;s to become expert testers overnight, pair with them. Do dev box testing and share your mental models around testing and automation. They would also open up and share dev contexts. In the end, both amigos come out stronger engineers.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1365310837351583753?ref_src=twsrc%5Etfw">February 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This one just speaks more towards tweet # 18

You need to become the Test coach of the team and help devs understand how to test, help them by
building smart tools and yet again, pair more with them

## 21. Test automation is a Software engineering activity

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">21. Testing and Test automation is an engineering activity, everyone on the product owns this and should do this. Don&#39;t let anyone tell you otherwise. 😉</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1365311450328096770?ref_src=twsrc%5Etfw">February 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Take pride in being a **Software craftsmen** and really care about your automation code.

> Remember: Every job is a self-portrait of the person who did it. Autograph your work with
> excellence - Ted Key, American cartoonist and writer

That means, you code should be **clean**, **maintainable, extendable** and should scale well

Writing well factored automation code is a craft and like Software development, you need to get
better at it over time.

How to get better at it, you may ask?

The good news is, there are literally tons of resources to get better at it. If you are looking for
one, Look no further than [Test automation university](https://testautomationu.applitools.com/) that
has tons of courses created by Automation experts.

Shameless plug, I have couple of courses on it already. Check them out!
[Courses by automation hacks](https://testautomationu.applitools.com/instructors/gaurav_singh.html)

## 22. Automate cases by priority and risk

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">22. Don&#39;t automate/execute your test suites from 1 to n. Identify the priority based on customer risks, Using data, find out which flows are critical and most used. Automate to mitigate those risks first and then go in a descending order</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1370649001293271042?ref_src=twsrc%5Etfw">March 13, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Last but not least, all Testing activities should always be in the order of their **impact to
customers**, and look at mitigating customer risk.

That means, don't take any easy shortcuts or quick wins! Cover your business critical cases first.

Some of these Testing activities to be done in priority order could be:

- Manually testing a product via scripted tests
- Executing an exploratory testing tour
- Automating a test case
- Running automated tests

and so on!

## Conclusions

> Phew! 😌 I really gotta stop writing such mammoth posts! but this one was a long thread and
> deserved some explanation 🙌

None of these should come as a huge surprise to you, but I hope your find these mental models useful
to you and your teams. I believe taking care of these would really result in some robust and
scalable automation. WDYT?

As always, Do share this with your friends or colleagues and if you have thoughts or feedback, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing and coding.
