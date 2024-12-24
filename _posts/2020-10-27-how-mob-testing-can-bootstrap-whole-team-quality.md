---
title: How mob testing can bootstrap whole team quality
excerpt:
  "Mob testing is a very useful testing practice to encourage the whole team to test together and
  more often and is really effective at finding bugs while teaching everyone about the wonderful art
  of testing. In this post, I share the format I personally follow and my observations about this
  technique"
permalink: /2020/10/27/mob-testing-bootstrap-whole-team-quality/
image: /assets/images/2020/10/duy-pham-Cecb0_8Hx-o-unsplash.jpg
categories:
  - "Software Testing"
tags:
  - "Mob testing"
  - "Testing fundamentals"
---

![Friends sitting together](/assets/images/2020/10/duy-pham-Cecb0_8Hx-o-unsplash.jpg)

<span>Photo by
<a href="https://unsplash.com/@miinyuii?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Duy
Pham</a> on
<a href="https://unsplash.com/s/photos/group?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>

Hi there,

Let me ask you this obvious question?

> Do you think devs, PM, designers, Business folks in your team can't test as well as you (the
> dedicated tester)?

If you answered yes to the above question, I would encourage you to think again.

From my own experience, I've found that given sufficient context they can test, and **to be honest**
**test quite well**, almost to the point where you (as the team's tester) can actually think of
taking a vacation and come back to business as usual with awesome products and features getting
shipped.

Now, You might be thinking, what is this guy talking about, this seems like wishful thinking and a
pipe dream at best.

But what if I were to tell you that there is a very simple practice you can adopt to ensure that
your team collectively gets better at testing and testing almost becomes _fun_ to a certain degree.

With that background context, In this post, I want to bring up one of the more effective ways that
I've tried in my team that works wonders in encouraging whole teams participation in testing, It's
called **mob testing**, not discovered by me of course, and has been written and talked about on the
[ministry of test blog by Maaret Pyhäjärvi](https://www.ministryoftesting.com/dojo/lessons/mob-testing-an-introduction-experience-report)
among many others I'm sure

## What is mob testing?

With mob testing, I'm not talking about mafia or gangsters here. 🔫 (Please excuse my bad jokes! 🙏)

Mob testing is a natural extension to **pair testing** wherein instead of a pair (2 people), we have
a larger group of people testing the app/system together and is quite wonderful in getting the whole
team engaged in the testing process while building shared knowledge and context

**Too many cooks spoil the dish** is a popular saying that might put a question mark on this being
effective but in this case, the group actually works to an advantage.

How you may ask? Well, I'm sure you'd agree that another pair of unbiased eyes are often quite
effective at catching bugs/design issues in either code/app. That is what testing is in most
contexts.

With mob testing, you get even more eyes that inspect the app at the same time and check different
facets of the system.

Below is the sample format that I follow within my team at Gojek and that has worked quite well. I
have tried this within the team mostly in consumer-facing mobile apps testing but this
format/technique is generic enough to be applied easily in different contexts

## The format

### Audience

- Should be a group of cross-functional engineer/product people(Dev, Test, PM, Business) which
  understand the feature on a high level

### Guiding principles

- A session should not be more than 1.5 hours, anything more might not be very engaging for the
  group or try to take breaks in between, whichever works best for your team
- Everyone takes a turn on the keyboard/mouse/device for a fixed duration, guided by a timer
- This approach follows a **Strong style navigation**, wherein the **driver** is not allowed to put
  his thought process behind the actions on the app/system, instead, his/her actions are guided by
  instructions from **navigators** in the group that take their turns.
- End the session with an optional and concise ~10 min retrospection to gather feedback on what
  could be improved for the next session
- Remember to be kind, considerate, and respectful to everyone in the group. Even though they might
  not understand much about the feature they are almost guaranteed to take away valuable context,
  Also try to clarify if someone has questions about the **System Under Test (SUT)** during the
  session
- Hear everyone's voice actively and be inclusive.
- Try to build on top of what's already tested by earlier navigators and check different aspects of
  the app

### Rules of the game

- The person on the keyboard is not allowed to decide what happens next
- Instructions come from the group should come at the highest possible level of abstraction

  - 3 steps form this abstraction: Intent, Location, Details
  - **Intent:** explain what we want in simple terms
  - **Location:** if the intent is not enough, then specify the location where action has to be
    taken
  - **Details:** Low-level details if needed

- Only the driver has permission to do actions, no one else should touch the keyboard/device
- We should take turns and every driver would be on the keyboard for **no more than 10 mins**
- To start with one person would be the **designated navigator** and this should be rotated
- Someone should take the role of **facilitator/time cop** and ensure the group remains focussed on
  the task at hand, this person or someone else designated _may_ take notes on any observations made
  by the group and summarize at the end
- The session should be largely **exploratory** in nature but you may give it more focus by coming
  up with **charters** or **tours** to explore in the session
- Once everyone is done with their turn, rinse and repeat until time runs out.

## Does it work

Absolutely, I've tried this with my team of devs, PM, designers and have received positive feedback
on this from everyone.

Not to mention this works wonders when you are developing a feature that has to ship soon since
everyone in the team sees the ground realities and this can be amazing for calming the nerves of
stakeholders and give an idea on release readiness.

I've observed this work much better than even a sprint demo since you actually get stakeholder
involvement in the testing process.

It's very useful in onboarding new folks in the team since they get to understand very quickly about
the **SUT** and can make use of the live session to ask questions.

As a very small metric, I've seen close to **20+** bugs found on an average on every session that
I've tried in my own team and frankly have observed **some really nice corner cases suggested by
devs/PM/designers in the team**.

The icing on the cake is that everyone on the team gets a peek into the mind of the tester and
realize it's actually a skill that you can learn provided you are open-minded and not a mysterious
dark art that many people might want to think of it as.

## Conclusion

I hope you would give this a shot and try this in your own teams and realize the value this practice
brings. If you want to learn more, do check out the blog on
[Ministry of testing blog](https://www.ministryoftesting.com/dojo/lessons/mob-testing-an-introduction-experience-report)

If you found this post useful, Do share it with a friend or colleague and if you have thoughts, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing.
