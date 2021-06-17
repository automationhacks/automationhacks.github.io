---
title: Testers are not the last line of defence
permalink: /2019/06/24/testers-are-not-the-last-line-of-defence/
categories:
  - Testing
---

Thoughts on why testers need to think beyond their role and evolve to become quality coaches for the
whole team.

![Things to test](/assets/images/wp-content/uploads/2019/06/david-travis-wc6mj0krzgw-unsplash.jpg)

Hello there,

If you are reading this and are in the software engineering field as primarily a developer or
tester, then I have some important thoughts to convey to both of you.

For Dev &#8211; \_Test is not your patsy to whom you can just hand over builds and offload any
concerns for the quality of you_r code.

For Test &#8211; _Your job is not to enable the above dysfunctional behaviour and act as gatekeepers
all the time._

Some of you might immediately contradict above since it is quite an opionated thought.

You might even say, <u>Well that is fundamentally what a dev or a tester has to do</u>! However
allow me to explain why this is just a bad idea.

Throughout my career i have seen the same thing play out numerous times often with bad consequences
for product quality.

## Bug ping pong/ Dysfunctional loop:

Does the below scenario sound familiar in any way?

1. Product managers/Business analysts comes up with a set of user stories/requirements for a problem
   business wants solved **(most of the time urgently or on a deadline)**
2. Developers gets involved from the start along with UX designer's/PMs and come up with
   ideas/implementation on what and how to build.
3. Testers are busy with either other deliverables (automating a mountain of backlog of tests) and
   are generally involved late in the game when product/feature is already built
4. Testers believing that they are the only champions **of quality** take a look at the app and find
   design issues and bugs (sometimes even in basic app flows and often times in negative flows or
   edge conditions)
5. Dev team is pleased and amazed to have such quality gatekeepers and fix these bugs and mostly
   ignore design issues as feature misses or differ them to a future release and hand over another
   build to the testers
6. Testers take another look and find most of the issues are fixed, however there are still
   regression bugs and report it back. (They get feeling of being validated at this stage and happy)
7. Dev's are either happy or annoyed that such bugs are being uncovered this late, though without
   having a real choice they work on fixing these issues.

&#8230;&#8230; And so the cycle continues on and on and on. . This is akin to a game of table tennis
or ping pong.

<hr class="wp-block-separator" />

I have lost count of how many times, I have seen this happen.

Do you see any problems with this? At first glance you might see this as **business as usual**
however there are deep problems with this.

## Testing anti patterns:

This most often than not results in below anti patterns:

1. Devs become complacent knowing that test will act as a safeguard and do not build enough test
   coverage (Unit/Integration)
2. Dev are mostly happy with basic sanity instead of rigorously exercising the build.
3. Test often acts as an enabler of this ping pong cycle and are mostly engrossed in multiple cycles
   of executions (in most cases manually in the interest of urgency to ship the feature or bug fix)
4. Very less automated tests are written leading to the mountain of test automation backlog.
5. Designers/PM's often are baffled as to why so many edge and negative scenarios are not thought of
   earlier
6. The whole process as such becomes an excercise in inefficiency.

<hr class="wp-block-separator" />

Here is a some food for thought:

<blockquote class="wp-block-quote">
  <p>
    How can a tester assure quality of a piece of code which is not authored by him.
  </p>
</blockquote>

Well, I hope the above arguments lead you to see the problem. However if this is such an issue then
what can we do to fix this?

We can certainly take action on below:

In a utopian world.

## Test stops acting as a gatekeeper:

Testers gets involved from the beginning of product design asking critical questions and also
encouraging entire team to **start thinking** on below lines:

- What is the feature we are building?
- Why are we even building it?
- Where is this going to add value to the customer and where will code changes be made?
- What all app areas would be impacted by this?
- Who are our customers?
- How will they use the product?
- Are we building the **product right**? Or are we **building the right product**? (Subtle but
  important)

## Coach developers into the art of testing:

Testers coaches developers into wearing the testing hat and help them to get into the habit of
thinking about breaking something that they themselves made by **pairing, being part of code
reviews, setting up and facilitating mob testing** or bug bashes and other such formats and
essentially help setup a culture of whole team ownership of quality.

## Setup automated tests and author them together

Testers helps dev team setup automated tests either at an integration or functional layer by
building easy to use frameworks and tools and dev also takes ownership of authoring functional
tests.

## Be part of code review

Testers sits as part of code reviews and inquire into the test coverage or even give pointers into
what conditions are missed so that they can be automated or tested at the correct layer.

## Analyze customer data to learn usage patterns:

Testers looks into the customer usage patterns along with UX/PM/Devs to understand and validate if
the created feature actually had the desired impact or not.

<hr class="wp-block-separator" />

_Isn't above a much better use of a testers time and creativity._

What we all need to realise at the end of the day is that two brains are better than one and every
human (whatever role he/she plays on an engineering team) is **inherently curious** and capable of
figuring out how stuff works or breaks.

Testers need to jump off their high horse a bit and be more pragmatic with their choices. Devs are
really more of their partners in crime than the enemy.

So let me leave you with a final thought. Next time when a dev hands you a build to test. what are
you going to do? 🤔

Fin!

<hr class="wp-block-separator" />

If you found this useful, why not share with a friend or colleague?

For more posts on test automation or testing theory check out automationhacks.io

Happy testing! Cheers!
