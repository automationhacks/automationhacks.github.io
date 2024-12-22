---
title: "TribeQonf 2024 Debrief"
excerpt: "Talks I saw and what I learned from them, tools and solutions explored at booths and the people I met"
permalink: 2024-07-14-tribe-qonf-2024-debrief
published: true
image: /assets/images/2024/07/tribe-qonf-2024.png
canonical_url: "https://newsletter.automationhacks.io/p/tribeqonf-2024-debrief"
categories:
  - "QA"
  - "Conferences"
tags:
  - "Conferences"
---

<figure class="image">
    <img src="assets/images/2024/07/tribe-qonf-2024.png" alt="Image showing a persons photo speaking at conference">
    <figcaption>The test tribe, TribeQonf 2024</figcaption>
</figure>

## Why read this?

I had the privilege of presenting a [talk](https://docs.google.com/presentation/d/e/2PACX-1vTpW84YaOPWIauhb4Iv7j1kv_iNR-PE_okDygXjgxmLs6qNd_tPPsJEvoAYsRmUTW5iG4LxxPG9-Nwv/pub?start=false&loop=true&delayms=10000) on [Mastering gRPC testing](https://www.thetesttribe.com/tribeqonf/gaurav-s/) at the TribeQonf 2024 conference on 12-13th July conducted at Radisson blu in the silicon corridor ORR bengaluru.

It was a fun 2 days of high energy, insights, and networking. I had the chance to hit some of the sponsor booths and chat with peer speakers and attendees, It was a pretty solid conference experience put up by The Test Tribe team

In this blog, I wanted to digest and decompress some of the advice and insights that I took away. Some of these validated thoughts that I have already had while others were novel ways of looking at problems.

I hope it is useful, and it would be fantastic also to hear your thoughts in the comments and if you were an attendee, what were your top takeaways.

I’ll break it down into a few sections to keep it contextual

* Talks
* Sponsor booths and what problems they are solving
* Networking with peers

## Talks

### Inside-out look at a Tester's success - Pradeep Soundararajan

[Pradeep](https://www.thetesttribe.com/tribeqonf/pradeep-soundararajan/) called out he faced challenging conditions but was able to thrive regardless as a tester by using them to his advantage

He explained how he was let go from different jobs before he was able to turn it all around by starting his own company. His journey into fitness, spirituality, and prioritizing his health with a holistic lifestyle while focusing on the 1% of things that are in your control vs all the other noise and chatter we tend to focus on really stood out to me.

Whatever we achieve in our careers is not solely due to our own efforts but also due to people around us.

We should focus more on living a holistic life than chasing the next promotion or title bump and deal with all the self-induced stress that comes from it.

Moolya and Pradeep were also kind to provide his new book **[Growth Driven Testing](https://www.amazon.in/Growth-Driven-Testing-startups-enterprises-ebook/dp/B0CLCPN1S4)** as part of the attendee kit and I’m looking forward to reading and learning more from it.

### AIoT is here testers. Are you ready for the challenge? - Vipin Jain

Vipin broke down challenges in the IOT testing space and how there are multiple challenges in different layers of the [OSI model](https://www.cloudflare.com/en-gb/learning/ddos/glossary/open-systems-interconnection-model-osi/). He explained how data aggregation is a key process and also provided an example of how AI could play a role in HealthTech for medical report analysis, alerting and providing patients care.

### AI-Augmented Testing: How Generative AI and Prompt Engineering Turn Testers into Superheroes, Not Replace Them - Jonathon Wright

This talk was super high energy

Jonathan played some AI-generated Hindi songs while graciously showing off his dancing skills on stage as well. No small feat if you ask me.

Jonathan works at Keysight which provides a platform for test automation on hardware and sensor devices. Keysight also acquired Eggplant which provides the ability to automate UI flows using computer vision technology and provides a low code solution to create automated tests using a UI

Jonathan suggested running GenAI models on local servers (or even a surface tab 😉) as a way to get leverage out of these tools without sharing your confidential data with big AI companies

He also reshared Tariq King's method of using markdown to provide a more procedural prompt to GenAI to get better results.

An example of this is shared below which was also built upon by Rahul Verma in [this LinkedIn post](https://www.linkedin.com/pulse/prompting-experimenting-markdown-example-test-data-generation-verma-toiuf/)

```markdown
# MISSION
Generate data in multiple languages for a given context.

# INPUT

1. A user registration page in a web app takes the following inputs:

* `First Name`
* `Last Name`
* `Date of Birth in dd-MonthName-year format.`
* `City`
* `Country`
* `Full Address`

2. The web site accepts data in multiple languages.

# STEPS

1. `Choose 10 natural languages which can typically have challenges in a multi-lingual websites.`
2. `Create a Language Table with Language and Challenges.`
3. `Create one example of user data for each language by incorporating the challenges identified in the context of user registration data.`

# RESPONSE FORMAT


1. `Language Challenges Table`
2. `Tests Table with Test ID, Language, First Name, Last Name and so on columns for each data item.`
3. `The response should include only the above 2 tables.`
```

### Building Harmony in Chaos: Orchestrating Agile Delivery in Startup Realms - Nishi GG

> “Pace is continuous; stress should not be” - Nishi GG

This quote stood out to me

Nishi provided practical advice on how to structure agile teams to deliver while not letting stress levels rise in startups

Some of her advice revolved around:

* Template for tracking sprint items with Dev, QA estimates and 2W daily Gantt to call out when Dev/QA and other activities would take place and reduce ambiguity
* Identifying a clear POD structure with a short or long-term charter and continuing or dissolving them when the business outcomes are met to focus on the next problem
* She mentioned why reserving bandwidth of senior engineers and architects is important for multiple reasons and how it could be used for engineering productivity goals
* Importance of having clear focus time for teams while not neglecting play and creative time as well and how a growth pod could be set to ensure engineers get opportunities to work on horizontal items instead of their vertical initiatives
* She talked about pair/buddy testing as an important ingredient of a successful agile team for all the obvious benefits it could provide
* How **Sprint - 1** automation model is followed in teams at Pictory

### Revolutionizing Quality Engineering: Breaking Orthodoxy, Shaping the Future - Sahil Puri

Sahil’s talk was packed with insights into the challenges in quality engineering space from the lens of a realist and had suggestions on what could be some pragmatic approaches to solve:

* Quality is everyone's responsibility
  * The key point was to not be defensive about the **“Why did we miss this bug?”** question but instead lead the RCA and truth seek on the gaps in your testing and delivery process and plug that leaking hole
  * Quality is an abstract term for some, it is better to index on ensuring testing happens at all phases of the cycle by stakeholders with test professionals helping to set adequate guardrails
* Look beyond just testing
  * Focus on the pre-development stage - understand the go to market (GTM) strategy, business metrics, and outcomes and feed that into your test strategy
  * Understand system design, implementation details, and the expected scalability to do better testing around functional and non-functional requirements
  * Keep an eye on post-launch metrics to learn whether solutions actually solved the problem and moved the metrics in the right direction, take those insights and feed them back into your delivery process
* Coding dilemma
  * Learn to code; it would be immensely helpful
* Speed vs quality
  * It's not always a tradeoff
  * Teams should index towards increasing release velocity while not sacrificing product quality by the use of priority and data to identify the right scope and automated processes
* Priority
  * Test engineers should develop their advocacy and sales skills to ensure they are able to convey value in language that business and leadership teams understand
* Focus on breath as well as depth
* 100% tests **should** not be automated
  * Focus on **should not** instead of **could not**
  * Focus on areas that can help you release faster with confidence instead of chasing a vanity metric
  * Identify a clear CI/CD strategy and also understand DevOps bits to have better control over the release and quality processes

### Pattern Thinking for Prompt Engineers: A Case Study in Test Design - Rahul Verma

Apart from the markdown method that Jonathan shared earlier, Rahul explained how even providing additional context by using **markdown bold** could lead to better outcomes, he also showed how learning plain text diagraming tools syntax like **Mermaid, and PlantUML** could be used to generate state transition tests

Changing the language to passive voice could lead to better outcomes while creating custom GPTs

### Navigating Your Career Journey: Strategies for Growth and Success - Ajay Balamurugadas

Ajay provided actionable advice on how career growth for engineers could look like in a very engaging talk

He touched upon

* The need to build a network of peers who could act as accountability partners and help you learn
  * You should ask **“When was the last time you tried something new for the 1st time?”**
  * A few book recommendations - Atomic habits, Deep Work, Extreme Ownership - Be the CEO of Your Life, So Good They Can't Ignore You
* Use of **5W1H** (What, Why, when, where, Who, How) and **5 why’s** as a method of thinking deeply about problems and solutions and additionally add **else**and **not**to be more critical in your thinking
* Use the disposable time during your workday to do some experiments about what activity you can do things differently.
* Resources:
  * [Ultimate Productivity Toolkit - Rahul Parwal](https://leanpub.com/productivitytoolkit)
  * [Test With Ajay](https://testwithajay.com/)
  * [How to Deal with Difficult People on Software Projects](https://www.howtodeal.dev/)

## Sponsor booths

It was amazing to see different companies trying to leverage some form of AI, GenAI solution in order take care of generating test plans and even code using existing UI frameworks. I hope to learn more about this space in near future and hopefully build some of these tools as well.

### DevAssure

[DevAssure](https://www.devassure.io/) provides interesting oppurtunity to generate tests using GenAI taking web app screenshots and figma mocks as an input. While they are focussing on web to start with this definitely seems like a start up to watch out for.

### BrowserStack

Browser stack apart from their device and web farm capabilities is building tooling in test observability space with a product already out called [BrowserStack Test Observability](https://www.browserstack.com/test-observability). The demo was quite interesting and could provide better insights into test automation metrics

### Keysight

[Eggplant Test Automation Intelligence](https://www.keysight.com/us/en/products/software/software-testing/eggplant-test.html) solution offers the user of computer vision to provide a smarter low code solution to automated web, desktop, and mobile apps

### BlinqIO

[BlinqIO](https://blinq.io/) offers an AI test engineer to provide capabilities for GenAI test generation using multiple underlying LLMs for web apps and API

### Catchpoint

[Catchpoint](https://www.catchpoint.com/) offers observability on network metrics like latency, response times, reliability by intrumenting mobile and backend systems. While they compete with other trace and monitoring tools like datadog and new relic. The ability to get feedback before builds are shipped to prod at different POP (points of presence) was interesting.

### Devzery

[Devzery](https://www.devzery.com/) solves fast autonomous API testing by leveraging GenAI to generate API tests with CI/CD integration

### TestSigma

[Testsigma](https://testsigma.com/) provides low code solution to take care of tests on web, mobile and even have a cloud device/web farm to boast about.

### FinerCircle

[Finer Circle](https://www.thetesttribe.com/finer-circle/) provides a niche community of testing professionals with courses, interest based cohorts and much more.

## Networking

One of the main benefits of a conference is that it brings smart like minded people under one roof and allows the merging of ideas

I was able to connect with some peers and industry experts and get insights from their rich and diverse experiences.

Capturing these for posterity and hopefully serve as a reminder for folks reading this to go out and talk and network with folks. You never know what these connections may manifest for you in the future.

* **Geosley Andrades,**Director AccelQ - we chatted about his experience of transiting from a testing professional to engineering manager to a director in product marketing space. How his hands on experience helps him in his new role.
* **Pradeep soundarajan**, CEO moolya about his personal life and early married life
* **Sahil puri** EM Zupee I enjoyed learning about his experience managing an engineering team at zupee, challenges in test automation space and QA, org dysfunctions. His talk was of course well delivered and really insightful
* **Shrini Kulkarni, ex Director** - we chatted about unit, integration testing and specifically use cases of consumer driven contract testing
* **Chakravati Singh** Automation Architect PhonePe about problems PhonePe is solving at mobile testing layer, pre submit stages and how PhonePe testing org has evolved. Understanding how a dedicated platform team solves automation problems was very interesting
* **Prem Kumar Nagaraj,** staff engineer Razorpay about his experience building tooling at CI/CD, security tools, test selection and his prior experience at amazon
* **Tushar sharma**, growth and marketing, The Test Tribe - we talked about community building, how testing communities are evolving and what are the pain points and challenges that finer circle is solving
* **Sayanthan Roy,** Architect at Amadeus about how a plan to transition testers into automation engineers could look like, the approach and challenges that come with working with legacy frameworks
* **Gunesh Patil**, Test architect, Ushur - I learned about technical challenges he’s trying to solve at his company in an interesting space on customer experience and engagement

And thats a wrap.

Pretty action packed conference.

I think it will take some time to digest the dense information overload and I have nothing but gratitude about getting a chance to experience this conference and would definitely encourage folks to attend this next time.

Please let me know if you have questions or thoughts in the comments.

Thanks for the time you spent reading this 🙌. If you found this post helpful, please subscribe to the substack [newsletter](https://newsletter.automationhacks.io/) and follow my YouTube channel (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time 👋, Happy Testing 🕵🏻 and Learning! 🌱| [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
