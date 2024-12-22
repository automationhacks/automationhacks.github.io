---
title: "Engineering practices @ Meta: #4 Engineers write automated tests, well mostly! 😉"
excerpt: "At meta, Software engineers/developers own writing tests for their features and code, They are supported by dedicated teams and a sophisticated test infra though"
permalink: 2023-07-09-meta-engineering-practices-engineers-write-tests
published: true
image: /assets/images/2023/07/christina-wocintechchat-com-7VmGD9XkYOU-unsplash.jpg
canonical_url: "https://newsletter.automationhacks.io/p/engineering-practices-meta-4-engineers"
categories:
  - "Engineering culture"
tags:
  - "Meta"
  - "Software Engineering"
---

At meta, Software engineers/developers own writing tests for their features and code, They are supported by dedicated teams and a sophisticated test infra though.

<figure class="image">
    <img src="assets/images/2023/07/christina-wocintechchat-com-7VmGD9XkYOU-unsplash.jpg" alt="A female engineer typing code on a laptop wearning headphones">
    <figcaption> Photo by <a href="https://unsplash.com/es/@wocintechchat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Christina @ wocintechchat.com</a> on <a href="https://unsplash.com/es/@wocintechchat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
    </figcaption>
</figure>

At Meta, Software Engineers author most of the automated tests that gets written.

Developers write unit, integration and E2E tests.

There are distinct Testing frameworks to enable them to write these in the most optimal way with multi quality gates like:

- Local and CI linters checking if standards are adhered to
- Optimized test infra and test services that engineers can use while authoring and running tests.
- The data is heavily instrumented with loads of options to derive metrics and its easy to plot beautiful graphs and reason about tests performance and reliability.
- Devs are notified and reminded to fix and resolve quality issues with their tests.

In most startups, there are separate Dev and QA roles with clear separation of responsibilities and while devs author some unit and integration tests, its quite rare to see devs also adopt E2E testing frameworks as first class citizens.

Meta clearly has a distinct engineering culture when it comes to this industry pattern.

Does this mean that there is no QA or SDET presence within the company at all?

Not really …

Meta is a pretty big company with multiple products and lines of business. I have come across engineers having the role of an SDET or QA but this is in certain products and verticals and not a universal phenomenon and I particularly experienced this while working for WhatsApp.

Large scale exploratory testing is mostly outsourced to companies than full time employees and there are QA Engineering Leads who co-ordinate and make sure this is done and managed in the most efficient manner possible.

There are also multiple platform teams who work hard to keep the test infra and frameworks pristine and scalable for thousands of engineers.

This approach has some distinct benefits, such as lot of tests being written for a change or feature. Since devs own automated tests they also are incentived to keep them of higher quality.

However even with all that, the tests are not immune to test flakiness and its still an area of work that teams actively work towards improving. The no of tests are huge, but are they really written in the smartest and effective manner? This is a topic for another time and reflection.

I also discussed a bit more about this practice in [this blog](https://automationhacks.io/2022-11-10-deep-dive-into-evolution-of-testing-organizations#an-automation-platform-team), Please feel free to read that for future context.

Thanks for the time you spent reading this 🙌. If you found this post helpful, please share it with your friends and follow me (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time, Happy Testing 🕵🏻 and Learning! 🌱 | [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
