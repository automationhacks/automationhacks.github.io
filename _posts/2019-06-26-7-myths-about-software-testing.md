---
title: 7 Myths about software testing
permalink: /2019/06/26/7-myths-about-software-testing/
categories:
  - "Software Testing"
tags:
  - "Opinion"
---

_Common misconceptions about testing and the people who perform it._

![myths](https://cdn-images-1.medium.com/max/1600/0*I-e-cxWuRvRbct55)

Hello there!

Being a tester in software engineering comes with its own sets of myths and stigma about the role.
This post is about the these misconceptions and i aim to hopefully give an inside perspective of
someone who has actually been through these woods and maybe help to change these.

Who is a tester in today’s real world you might ask? Well, one of the MD of my current company had
below profound thought to share.

<blockquote class="wp-block-quote">
  <p>
    A tester is a cross between a developer and a product manager with a healthy dose of paranoia — <a href="https://medium.com/@ponnappa" target="_blank" rel="noreferrer noopener">Sidu Ponnappa</a>
  </p>
</blockquote>

### 1. Manual testing is non technical and easy

As harsh as it sounds, this is where most of the **stigma** comes within testing as a
skill. People who are doing manual testing are thought of as less technical as they are in most
cases are required to black box test the application using the UI like an end user would do.

Is this true?

Well, Yes and no. Testing can be \_as technical as the individual so desires \_given a
simple fact, If he has the **right mindset to look**.

A person doing testing need not restrict himself to just UI testing. There are many different areas
where a tester can add value to app development
(API/DB/Contracts/Integration/Unit/Performance/Security) and so on. All of these areas requires
someone to go in, understand how the nuts and bolts work and then find ways of identifying the gaps
and **_“break” the system_**

Obviously the above requires a lot of technical skills and tool knowledge and are quite tedious.

### 2. A tester is born with special skills and is the “ONLY” one who owns quality {#37c4}

This one bums me out not as much when it comes from devs but rather from testers themselves.

Throughout my career i have seen/faced this situation where devs who are not motivated enough to
test their own code would throw each and every small change to the tester to verify and the tester
would find some issues/bugs in this code. This is followed by self validation and euphoria and the
dev and test repeat this cycle for endless no of hours.

Testing is not a magical skill which only a select few individuals posses or can master. We are not
special snowflakes. Anyone who believes this is just wasting his and his peers time.

<blockquote class="wp-block-quote">
  <p>
    <em>Developers can test code, PM can test and so can a tester. Anyone who has the right testing mindset and is curious about how stuff works/breaks can contribute to this effort.</em>
  </p>
</blockquote>

Let’s take this with a grain of salt. Some activities are better guided by a person who specializes
in testing and can move the team towards a culture of quality but this in no way concludes that it
is the testers who own quality.

Now if both dev/testers would do each other a big favor and get their heads out of their asses and
work together we would have a much better team and quality product at the end of the day.

### 3. Testing is just verifying the app from the UI {#4ffe}

<blockquote class="wp-block-quote">
  <p>
    “You are introduced into a new project with no test coverage, what would be your approach?” — Asked a tester to another
  </p>
</blockquote>

If you ask the below question to someone who is getting started with testing and automation, chances
are you would hear something like below.

<blockquote class="wp-block-quote">
  <p>
    Well, I would just test and automate every case on the UI using selenium/appium or equivalent tool — Answered the tester
  </p>
</blockquote>

Did you spot the mistake in above approach?

Well for starter,

- It completely inverts the automation pyramid. The intent for testing something should be to get as
  quick of a feedback as possible and UI tests completely beat that intent
- Also this creates a dysfunctional scenario wherein someone has to maintain and debug all these
  1000+ long running tests that **_oddly_**_sometimes fail.
  Gosh!_

![](/assets/images/wp-content/uploads/2019/06/1d5f3-0qx6agf7s7ucpucxl.png)

Yes you can parallelize the executions on a cloud provider and throw more VM’s or containers at the
problem but that does not change the fact that successfully getting lot of value out of UI tests is
indeed a very challenging task with low ROI in most cases.

Instead if more API, Contract tests, Integration, Unit tests are written with only a cherry pick of
UI tests on top it would be a win win for everyone.

### 4. Manual testing and test automation are two separate entities {#23ec}

There is a bit of a great divide in the testing space where folks identify themselves largely as
either a Test automation engineer (a.k.a SDET) or a manual tester and generally automation skills
are more sought after than manual testing skills. Few folks even brag about it. On the other end of
spectrum folks are reluctant of picking automation skills.

In reality though what seasoned testers realize is:

<blockquote class="wp-block-quote">
  <p>
    <strong>Test automation is just a means to an end. Not THE END in itself.</strong>
  </p>
</blockquote>

Manual exploratory testing is a large precursor to automation and requires a high degree of
curiosity factor and ability to not look at a feature/app with inherent biases.

Automation is just another tool in the kitty bag of a skilled tester to get rid of tasks that are
boring or repetitive or delegate computations that is better done by machines as an example would
you like sniffing through thousands of lines of logs to identify some error patterns? Surely a
machine can do this better.

It’s silly to think test automation kills jobs for a manual tester when it is there to make life
easier. No one person can test 100 micro services with 10 conditions each every night. It’s not
practical or possible even.

In essence manual testing and automation are really ally’s fighting the same war.

### 5. Test Automation is not “development” {#26af}

Lots of testers believe they need to understand just the basics of programming to be able to succeed
with test automation. As long as tester can write crummy code that does the job
and **works** it is acceptable.

_We don’t need patterns or clean code. A test function which is 100 LOC long is perfectly fine since
we are not “real” developers anyways_

Right? right?

#### Wrong. {#0bff}

<blockquote class="wp-block-quote">
  <p>
    Code is code. Regardless of who writes it.
  </p>
</blockquote>

We face challenges like below:

- The act of crafting meaningful automated tests requires understanding the feature behind it
  thoroughly and to ensure we assert code at the correct level using functional or non functional
  aspects. This requires sound dev skills.
- We need to write maintainable, extensible frameworks which are intuitive for others to follow and
  allow the testing efforts to scale.
- Choice of programming language with an ecosystem that supports the needs of different projects,
  developing POC’s, using IDE’s, working with build tools, CI, test frameworks as well as setting up
  telemetry using different reporting solutions are all activities which take good amount of skill.

How are these any less challenging than writing a backend service or a UI using some framework
sometimes baffles me? It’s no less and should not be treated any less.

Testers also need to understand that anything less than clean code should not be acceptable and we
need to understand sensible dev practices and patterns if the framework/harness has to scale.

<blockquote class="wp-block-quote">
  <p>
    <strong>Everyone is a developer and should aim have the same set of technical design/coding skills </strong>to be efficient.
  </p>
</blockquote>

### 6. Everything needs to be automated {#25af}

This is a common misbelief among people who do not understand testing enough that if you have 1000
cases asserting your app then every last one of them needs to be automated.

What people learn from experience is that every new test that is added adds its own maintenance
costs. Experienced people who have got their hands down in the trenches know that **Test
selection and prioritization** i.e choosing what to automate and when is an essential skill and
can make all the difference between successful or failed automation projects.

### 7. As a tester, we should be isolated from devs and should not look at dev code/PRs/Unit tests {#f4e8}

Have you seen cases like this?

- _Tester will ask the dev if he is writing enough unit tests for the feature and would be satisfied
  with just a verbal response?_
- _Tester would \_rarely_ take a look at created code in different pull requests?\_
- _Testing is treated as a separate discipline and feel they should test everything from outside the
  box_

All of these are in some shape or form myths or old practices which does not have much of a place in
the modern software engineering world.

Agile as a core tenant advocates for “Whole team” approach wherein teams really are cross functional
and **can and should** collaborate on code

As a tester. There is really nothing wrong in getting code access to the app that you are testing
day in and out to get an insider perspective of how it really works. Or giving comments on PRs. It
is acts like this that help bridge the gap between dev and test. You might not understand each and
every component but you might be surprised by the value you can bring to the table with
your **systems thinking mindset**and ability to see impacts beyond the immediate code,
Often times a dev deep in his act of creation misses basic or edge conditions which are often better
captured as a unit/integration test.

Well, you as a tester can help identify and **even fix** these issues.

<hr class="wp-block-separator" />

And that it folks!

What do you think about the above? I am curious to hear your thoughts on this. Hopefully this post
helps in a small way to clear some of the myths around testing.

If you found this useful in any way. Why not share it with a friend or colleague.

Until next time. Keep breaking stuff! Cheers!
