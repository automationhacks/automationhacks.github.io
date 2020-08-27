---
id: 957
title: Writing clear bug reports
date: 2020-07-25T15:03:51+00:00
author: Gaurav
excerpt: 'Writing clear and concise bug reports can greatly reduce the back and forth between different engineering stakeholders. We discuss on what makes a good bug report and I also provide a template that I use. '
layout: post
guid: http://automationhacks.blog/?p=957
permalink: /2020/07/25/writing-clear-bug-reports/
jabber_published:
  - "1595689433"
timeline_notification:
  - "1595689437"
email_notification:
  - "1595689437"
image: /wp-content/uploads/2020/07/undraw_bug_fixing_oc7a.png
categories:
  - Testing theory
---
<figure class="wp-block-image size-large"><img loading="lazy" width="750" height="562" src="https://i1.wp.com/automationhacks.blog/wp-content/uploads/2020/07/undraw_bug_fixing_oc7a.png?resize=750%2C562&#038;ssl=1" alt="" class="wp-image-970" data-recalc-dims="1" /><figcaption>Bug fixing on [unDraw.io](https://undraw.co/) Created by <a rel="noreferrer noopener" href="https://twitter.com/ninaLimpi" target="_blank">Katerina Limpitsouni</a></figcaption></figure> 

As a tester/developer, Once you find a bug in the system under test, the next logical step is to either fix it (if it&#8217;s really that small 😉) or to write a bug in the bug tracking system of you choice to allow yourself or one of your colleagues to take a look and fix the issue.

<blockquote class="wp-block-quote is-style-large">
  <p>
    A well written bug report saves a lot of headache to all parties involved.
  </p>
</blockquote>

<p class="has-drop-cap">
  TLDR; If you are looking for a template to follow in your projects, Here is one that I came up with inspired by many other testers and some open source projects. Feel free to remove sections and their explanations if they are not relevant to your context.
</p><figure class="wp-block-embed is-type-rich">

<div class="wp-block-embed__wrapper">
  <div class="gist-oembed" data-gist="87b62440faf36d98ebbb732c372dd7c3.json" data-ts="8">
  </div>
</div><figcaption>Bug template to help in writing clear bug reports</figcaption></figure> 

Read further to understand what constitutes a good bug report and some tips on how to come up with them.

## What are the necessary details?

If you see most of the bugs logged in a system, they are often written in a hurry with very less attention to the details, In most cases probably with a **one liner title**

This can lead to a lot of frustration for the person who looks at it next because they don&#8217;t know some of the important details and then have to put their **sherlock holmes** hat and search for answers and this often a lot of back and forth between Dev/Test/PM to figure out the area where the issue is present.

Some of the common questions that a person asks when trying to fix a bug in a typical consumer/business facing app for web/mobile/backend system are mostly along the lines of. 

  * **When** does this bug occur? How can they **reproduce** it?
  * **What** is the buggy behavior and what was **expected**?
  * What is the **impact** to the user? How **critical** it is to fix? Decide on Now or later?
  * Does this happen with a **specific test data** only?
  * What **build** was used to test this (ideally tagged to a git commit)
  * If the bug is on **mobile** then what was the **mobile, viewport size, OS** details?
  * If the bug is on a **browser** then what is the **browser type, resolution, version**?
  * If the bug is in an **API** then which **specific API/business flow** is impacted, what are the request params and response?
  * **Screenshot** with a **marked up area** which is buggy?
  * **Video** showing the steps to arrive at the bug?
  * Application/Server logs?
  * Any specific feature toggle/configuration that was in play when the bug occured?

and many more depending on the context.

## Moral responsibility as a bug advocate

I would argue that you should aim to give as **much details as possible** in your bugs limited only by the time available/context and to always do a bit of upfront analysis before raising a bug.

Doing this sets you up to act as a strong advocate for a bug fix and overall less headache all around for everyone.

A bug with very minimal detail is probably going to be pushed further down the Product Backlog and sit in oblivion being ignored because neither the PM nor the dev would be able to understand what is the issue or be able to analyze further. 

And we don&#8217;t want that now, do we? 🕵🏻‍♂️

<blockquote class="wp-block-quote is-style-large">
  <p>
    <strong>The devil is in the detail</strong>s
  </p>
</blockquote>

## Some tips for writing good bug reports

Now that we have established the _need_ for writing _clear bug reports_, here are some good intentioned bit of advice with some specifics on what you can do better next time you write a bug report.

### Take a deep breath first and then start investigating

When you see an **obvious bug** in the system, the typical knee jerk reaction from a tester/developer is, _&#8220;What was the person who developed this thinking?&#8221;, &#8220;This is really silly, How could they have missed this in their unit/integration tests?&#8221;_ yada yada and so on &#8230;

I know, _we&#8217;ve all been through this_ during our careers. 

But, I urge you to take a moment and a deep breath and calm down first.

What you should understand and realise is that most commonly a bug manifest itself at different layers of the stack and under specific conditions which could comprise of multiple factors 

All of those conditions **cannot** be simulated at an unit/integration level. Sometimes the dev is under high pressure to release the feature under a deadline and as such tests only the bare minimum functionality.

<blockquote class="wp-block-quote">
  <p>
    It&#8217;s human to make mistakes and some of us are more human than others.
  </p>
  
  <cite><strong>Ashleigh Brilliant</strong></cite>
</blockquote>

We should understand the human factor at play here and try to separate the **individual** from the buggy behavior. 

With that little bit of empathy, The next step is to gather **more** evidence along the lines of the **necessary details** mentioned above and draft them in your bug report. **Remember**: _It&#8217;s perfectly okay to edit and revise with more details as you investigate_ further.

Let&#8217;s take an example of an investigation flow:

If the bug is on a UI (app/browser), ask yourself is this purely a presentation issue on the UI or because of a bug in the business logic with the underlying API, What and how can I check to determine and find a root cause for this?

You should open up network tab on chrome dev tools if a browser or a suitable proxy tool like Charles/MITM to view the network calls made and see whether you can gather more information:

  * An API call was made with the correct request parameters (URL, Header, Query, Body)?
  * Did a response come back in time?
  * Inspect the response data for any incorrectness in status codes/response body
  * Inspect the relevant database tables to see if any incorrect data was written (if needed)
  * Check the application logs for the backend system
  * Is the really service up? Going through a deployment?
  * Did a dependant service fail.

In conclusion, 

<blockquote class="wp-block-quote is-style-large">
  <p>
    It&#8217;s often quite useful to bucket a bug as either a Frontend or backend issue so that you can then tag the relevant teams/people to look into and fix the issue
  </p>
</blockquote>

**Capture these details in your bug report**. 📝

Doing all the above steps exposes a lot of internal details about the system that you are testing and makes you a better tester and product expert in the end.

## Write clear steps to reproduce

Often times we as testers think, it&#8217;s **quite obvious** on how to arrive at this particular screen/page/business flow. But remember, _what&#8217;s obvious to you might not be so for others or people who are new to the system_.

Do everyone a favor and write clear steps on **how to reproduce the issue**. You can even capture some common flows as templates in your note taking app and copy paste them if you see repeated patterns of bugs in screens.

Some details that you can add apart from repro steps to support.

  * Add screenshots (**marked up to the specific problem area**, don&#8217;t be lazy, a problem in the bottom right corner would not be obvious to the person reading your bug report)
  * Even better, add a video to show the flow. Trust me, this is super helpful and your Devs/PMs will really thank you for it.
  * Provide the CURL for the API call and the response that you saw from the API with the status code information.

This is even applicable when writing bugs for open source projects. Creating a small project that demoes the problem and attach it as a reference is so much better than giving an obscure description of the problem.

## Provide Version/Build details/logs

Okay, So you have done the due diligence and explained what the bug is, what&#8217;s the impact and its priority and now have clear steps to reproduce. 

We should be all good now, right? 😌 Well, almost there!

Often times bugs are quite related to specific conditions like the **browser, mobile, their viewport** or the **deployed commit/branch**. 

Adding these details gives a very reliable hint into the state of the system and can point the dev in a better direction to investigate further.

For instance, Within mobile context, The bug can be happening on specific **Device and OS combinations** and can provide a hint to the mobile dev on what specific libraries/frameworks are involved for that version.

For a backend dev, the Git commit detail could be especially useful since they can know immediately what branch was deployed on the environment and help them isolate the issue to fix. Also providing the app logs could be helpful since most logging frameworks mention the specific application area the log was generate in and could save a lot of time for the dev.

## Conclusion

Writing clear bug descriptions makes it super easy for project members to collaborate better while triaging and fixing bugs.

So the next time you see a bug, I hope you would write a better bug report. 😉

If you found this useful, do share it with your friends and colleagues. If you want to add your thoughts on this topic, Feel free to hit me up on twitter at @automationhacks.

Until next time, Happy testing and coding. 😇