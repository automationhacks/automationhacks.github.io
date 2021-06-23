---
title: Simple truths of Software Testing and Automation
excerpt:
  "Software testing and Test automation is nuanced field. There are many common sense truths that
  engineers should take care. This post elaborates on a twitter thread an the same topic"
permalink: /2021/06/23/simple-truths-of-software-testing-and-automation
image: /assets/images/2021/06/undraw_people_search.png
categories:
  - Testing
  - "Test automation"
tags:
  - "Testing"
---

<figure class="image">
  <img src="/assets/images/2021/06/undraw_people_search.png" alt="Lady searching with a microscope">
  <figcaption>Source: Undraw by Katerina Limpitsouni</figcaption>
</figure>

I started a twitter thread sometime back, capturing some simple insights about Software testing and
test automation.

Most of these are boring, common sense facts about practices in Software testing and have been
spoken and blogged about heavily.

I thought I was reiterating the obvious in that thread and it sure was fun to do a mind dump of
these common practices and tips

Some people appreciated this thread and asked to write this as a book, To be honest they are quite
short for a book but definitely deserve a blog post.

So here we go. Let's do this. 💪

I'll post each tweet and explain or give some additional context about each.

## 1. Early involvement

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Simple things we know to be true about Software testing and automation but often forget.<br><br>1. Involve testers right from the start of a feature and involve in the design process to get valuable feedback and better refined acceptance criterion's</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339944159658930179?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Smart testers possess lot of **business context**, when you involve them early, they can really help
you find gaps in your specs, such as missed requirements, corner/edge cases that were not considered
in initial design. You get all these right during planning and design phase for free.

In the end the product is better off, This also reduces these missed feature tickets during actual
testing phase

> 💡 Testers: Don't sulk and wait to be included if you are left out. I often find self inviting
> yourself to these discussions leads to paving a path for future.

## 2. Shift left

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">2. Shift quality and automation left, that means Dev&#39;s also write automated tests, testers look into design and UX much early and even start laying foundation for automation much early.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339944564006604800?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Why should testers have all the fun?

No, really! ...

Yeah, I know some testers have this **batman, (read superhero)** complex, They believe they are
bruce wayne that will save the burning gotham city (read **product**) from clueless devs that ship
untested code full of bugs,

But this is not how real successful projects scale. If you believe in QA as being the gatekeeper,
please read [Testers are not the last line of
defence]({% link _posts/2019-06-24-testers-are-not-the-last-line-of-defence.md %})

Testing is a team sport, and dev and test are really two sides of the same coin

An app that is released without **testing** is mostly gonna be quite bad and full of bugs, who does
the testing is another story altogether.

I'll give you a hint:

> Quality is everyone's responsibility

Devs should also be comfortable with the **automation code** and be able to add coverage or modify
as needed. Most rockstar devs that I know are more than interested in achieving this, you as the
tester just need to help them out with required context

Another side benefit of this is that Testers get **more time** to create robust automation and,
everybody wins this way!

## 3. Don't test automated cases manually

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">3. Don&#39;t repeat manually what is already automated, it doesn&#39;t make any sense. Use the time to test different things and unexplored areas</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339944746135900163?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This is really simple, but often overlooked. Some exploratory testers lack confidence in automation
and they would often repeat the same cases by hand.

To me, this is just wasted effort and diminishes the value proposition of automation. We should
strive to build robust automation and use the freed up time to test different tours or charters.

## 4. Build automation early

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">4. Cost of test automation is amortized with every CI run, build more automation and early. You&#39;ll get more breathing space plus machines are damn good at these repetitive tasks</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945076433199105?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I wrote about this in an earlier post, but you should strive to write some automation early and put
it in CI, this way you can very quickly run this suite to gain confidence about your system.

And trust me, Nobody, ...

I mean nobody likes to run same 10 cases every 1 hour for every new dev build. Its much better to
automate these and get them off your plate.

[Further Read: Why you should automate tests
early]({% link _posts/2020-03-21-why-automate-tests-early.md %})

## 5. Exploratory over scripted tests

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">5. Use manual testing for areas which really need it, accessibility, privacy, really hard to find bugs in untested corners, let your exploratory testers do what they do best, well explore the system. Don&#39;t make them execute repeated test scripts</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945343153160194?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Manual exploratory testing is really valuable, it involves someone using their mind, prior context
about the product to explore, slice and dice the product from multiple angles and often finds very
hard to discover bugs.

If you ask your testers to run the same scripted tests, will they take the uncommon sad path?

In most cases, no, so we should automate these predictable cases and unleash our testers to explore
the product.

Also exploratory testing is not monkey testing, it is a well structured methodology and involves use
of well defined tours and charters to cover a focussed subset of the product.

You can read more about it in amazing books like
[Explore it!](https://www.goodreads.com/book/show/15980494-explore-it) or
[Exploratory software testing](https://www.amazon.in/Exploratory-Software-Testing-Tricks-Techniques/dp/0321636414)

## 6. Automate boring stuff

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">6. Please automate the boring repetitive stuff</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945442142916609?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Quite obvious, don't repeat the same `n` cases manually, automate them.

Have to create some test data again and again, don't do it manually, write an automated script

Takes lot of time to do X, well you know what to do 😉

## 7. Start small and Iterate

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">7. For your frameworks, Please start small and iterate. Keep it simple and don&#39;t do a big design upfront. To enough to get a good picture and get started but don&#39;t write a thesis.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945758229860357?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I've found doing big elaborate design upfront (`BDUF`), or writing long documents usually does not
lead to good frameworks or tests. Obviously this might not hold true in every single context, but
its better to start really small and then quickly iterate.

Remember refactoring is your friend here.

Do enough design to form a good high level idea but don't really go deep into each component. Let
the coding surface some of these low level details and then pivot appropriately.

## 8. Respect test pyramid

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">8. Write unit tests, check the integration points/contracts, Test your API endpoints, with a little bit of UI automation on top.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339945945220280320?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This one just describes the classic Test pyramid. Its a really good idea to write the appropriate
test at the required level.

And yes, you as a test automation engineer should go deep into the product stack and understand how
to write these tests. Don't limit yourselves to only Functional E2E tests.

If you want to know more about this, read
[Test pyramid](https://martinfowler.com/bliki/TestPyramid.html),
[The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) at Mr
Martin fowlers website

## 9. Write atomic tests

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">9. Don&#39;t write long tests. They will be anyways be flaky</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339946031555858432?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I don't think this needs explanation, don't write tests longer than 10 Lines of code. Even that is
long in most contexts.

Write small, focussed tests that do one thing and assert its outcomes

## 10. Build parallelization from the start

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">10. Design automation with tests concurrency in mind</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339946135868252160?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

As soon as you have 5 sequential tests (for a new framework), spend some time and make them run in
parallel.

It can be a bit of work initially but the payoffs are huge. When your suite has 10, 100, 1000, 10000
tests, effectively designed parallel suites will win every single time.

## 11. Design smart coverage

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">11. You don&#39;t need to test everything in all possible ways, just enough coverage to increase confidence in your releases.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339946330387431424?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This one is subtle, every single test that you'll add to your suite has a test maintainence
overhead. Treat your automated suite or tests like a garden and regularly prune them to remove any
redundant unnecessary tests. Usually writing very targeted tests that business cares about is the
smart thing to do.

Don't fall in the metrics trap. 90% automated tests, 95, 97 and so on ...

Ask yourself, can I write `n` no of smart tests that give me lot of coverage and are really give me
and the team the confidence to release features early

## 12. Test sad path more often

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">12. We mostly test happy path so much, but ignore the sad path. Test that more.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1339946482284126219?ref_src=twsrc%5Etfw">December 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I really should not explain this, but most testers are busy ensuring happy path works, and they
should. Hopefully you would have had smart automation built to cover this.

What often gets ignored are the corner cases, on that unique Test/OS/screen size that often cause
lot of customer angst. Please test that more, find more time to spend on these.

## 13. Write hermetically sealed tests, should fail to detect a change

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">13. Tests should be small, focussed on testing one thing only, and isolated from each other, in order to be easily parallelizable and be deterministic. If the test fails, it should detect a change in the system.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1340208018311446530?ref_src=twsrc%5Etfw">December 19, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

We already spoke about this in tweet # 9 and 10, however let me add few more aspects, never ever
write tests that share some common data, because they inherently force you into a sequential suite
and we don't wat that do we?

Also spend time and write good assertion messages, when your test assertion fail, and trust me, they
will, you should have a friendly message that explains where exactly it went wrong. Its one of the
most important things to get right, please spend time on this simple habit and the rewards would be
really good change detecting suites

Needless to say, when you tests fail, make sure someone detects and reports it to appropriate dev to
get it fixed.

## 14. Keep your suites healthy

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">14. Continuously failing tests just leads to product teams ignoring the tests. Value of automated tests goes down drastically at that point. Fix any flakiness, raise bugs if the test fails.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1340208614464577536?ref_src=twsrc%5Etfw">December 19, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Automated tests are not magic, we often say, that suite is flaky, it keeps on failing all the time.
If this keeps on happening, you have failed in your automation efforts.

Don't write new tests to show some coverage increase metric to management.

Every failing tests is an opportunity to explore what exactly went wrong. You either find a product
bug, problem in your environment or just and opportunity to design a better test, please don't just
re-run the test and ignore it saying it passed now.

## 15. Before automating, test it manually

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">15. To automate something, you have to test it by hand first, to understand how it works, its nuts and bolts, its failure points and then &quot;choose&quot; what makes sense and adds value before going ahead. Don&#39;t be in a rush to code. Think twice code once. 😉</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1340489072121298946?ref_src=twsrc%5Etfw">December 20, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Here is a silly phenomenon, we harp on automated tests as the savior. As an individual contributor
it sure is fun to churn out code and automated 5 - 10 cases per day. Everyone appreciates such an
SDET right?

However, if you are doing this activity just for the sake of it, or the praise. In most cases its
not really effective automation. I'll encourage you to understand the context behind the feature you
want to automate first and test it once or twice manually.

Ask yourself:

- Is there any value in automating this?
- Is this better off being tested manually?
- Do I understand this feature enough?
- What sort of assertions should this test have?
- Should I break this down into multiple smaller tests?

This would ensure that when you get down to writing the automation, you already have a good mental
model about the feature and can write better tests. Also, don't forget to write documentation to
help the next engineer who looks at this feature.

## 16. One size doesn't fit all

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">16. The approach that worked in one project might not in another project/org. Keep an open mind. Evaluate couple of automation tools before deciding on the best one for your specific needs and context. <br><br>&quot;If all you have is a hammer every thing looks like a nail&quot;</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1340490128880357378?ref_src=twsrc%5Etfw">December 20, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This has to be the most common mistake most Automation engineer make, does this seem familiar?

A new SDET joins your team, after looking at the codebase they say, the code is very badly written,
we need to rewrite this and build something from scratch.

Oh no 😱, Not another rewrite.

Quite often, these folks copy paste code from their last company codebase without thinking if it
really fits the need of the current team or company. Or someone has a favorite language and wants to
write everything in Java

Stop please, before you shoot yourself in the foot. Read this

Every team, project, company is different. Joining a new team is wonderful since you can start a
fresh. Take time and understand all the context before you jump in and start making suggestions.
Quite often, you'll learn a lot more this way and also the changes you make would be constructive
and not destructive in nature

I've made this mistake and learned from this. 😉

## 17. Asking right questions at the right time

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">17. Good testing is often asking the right questions, to the right persons at the right time!</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1350289376287154176?ref_src=twsrc%5Etfw">January 16, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Testing is mostly about asking really good questions to the right people at the right time. So the
next time you have a project kick off meeting, don't just sit there with your camera turned off and
read something else or write yet another automated test.

Take an active role in the meeting, ask really good questions, this way you can ensure lot of good
testing happens before even a single line of code is written

## 18. Pair with devs more often

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">18. 3 ways to get developers to test more and better:<br><br>- Sharing: Share your AUT knowledge and tools<br>- Pairing: Ask what have you already tested? What&#39;s remaining? What is worrying you?<br>- Caring: Coach them with care.<br><br>Taken from <a href="https://twitter.com/alanpage?ref_src=twsrc%5Etfw">@alanpage</a> <a href="https://twitter.com/hashtag/testflix?src=hash&amp;ref_src=twsrc%5Etfw">#testflix</a> talk<a href="https://t.co/FTkjtp7wer">https://t.co/FTkjtp7wer</a></p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1365300798398156800?ref_src=twsrc%5Etfw">February 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I think Alan page described this quite well and I'll recommend you to check out his talk on Test
Flix on how to encourage devs to test more and often.

In short, pairing with devs is going to be the most valuable skill you'll ever learn as a test
automation engineer. Do more of it!

## 19. Trust me, it will work, you only need to test this

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">19. If the dev says: &quot;You don&#39;t need to test &quot;x&quot; aspect of the app. Is should work fine&quot; <br><br>Confirm this assumption and do test around to discover regression impacts. More often than not, You&#39;ll be surprised to know cases that were not considered.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1365310305446756354?ref_src=twsrc%5Etfw">February 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

If you hear your devs suggest this, please ask them why they think this way and do they have any
proof of validating this assumption

Make sure you regression test every feature and never be satisfied with just testing the one change
that was made. It is tedious but often code breaks in other integrations rather than the component
that was changed directly

## 20. Pair some more

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">20. Don&#39;t expect Dev&#39;s to become expert testers overnight, pair with them. Do dev box testing and share your mental models around testing and automation. They would also open up and share dev contexts. In the end, both amigos come out stronger engineers.</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1365310837351583753?ref_src=twsrc%5Etfw">February 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This one just speaks more towards tweet # 18, You need to become the Test coach of the team and help
devs understand how to test, help them by building smart tools and yet again, pair more with them

## 21. Test automation is a Software engineering activity

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">21. Testing and Test automation is an engineering activity, everyone on the product owns this and should do this. Don&#39;t let anyone tell you otherwise. 😉</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1365311450328096770?ref_src=twsrc%5Etfw">February 26, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Okay, this shouldn't really come as a surprise to you but Test automation is a pure Software
engineering activity, don't let some unmotivated frustrated engineer tell you otherwise. Take pride
in being a Software craftsmen and give complete care while writing your automation code.

That means, you code should be clean and should be extendable and scale well

Trust me, Its a craft and like Software development, you need to get better at it over time.

How to get better at it, you may ask?

The good news is, there are tons of resources to get better at it. If you are looking for one, Look
no further than Test automation university that has tons of courses created by Automation experts.
Shameless plug, I have couple of courses on it already.
[Courses by automation hacks](https://testautomationu.applitools.com/instructors/gaurav_singh.html)

## 22. Automate cases by priority and risk

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">22. Don&#39;t automate/execute your test suites from 1 to n. Identify the priority based on customer risks, Using data, find out which flows are critical and most used. Automate to mitigate those risks first and then go in a descending order</p>&mdash; Gaurav Singh (@automationhacks) <a href="https://twitter.com/automationhacks/status/1370649001293271042?ref_src=twsrc%5Etfw">March 13, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Last but not least, all Testing activities should always be in the order of their impact to
customers, and look at mitigating customer risk. Going with the highest priority

Some of these activities could be:

- Manually testing a product via scripted tests,
- Executing an exploratory testing tour
- Automating a test case
- Running automated tests

## Conclusions

None of these should come as a huge surprise but I hope these are useful to you and your teams.

As always, Do share this with your friends or colleagues and if you have thoughts or feedback, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing and coding.
