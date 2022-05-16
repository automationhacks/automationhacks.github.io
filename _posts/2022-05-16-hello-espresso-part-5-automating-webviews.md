---
title: Hello, espresso! Part 5 Automating WebViews 🕸️
excerpt: "Learn how to automate hybrid apps with WebViews using espresso web"
permalink: 2022-05-16-hello-espresso-part-5-automating-webviews
published: false 
image: /assets/images/2022/05/espresso-part5.png
canonical_url: ""
categories:
  - Android
  - Espresso
  - "UI Automation"
tags:
  - "Mobile Testing"
  - "Android Testing"
  - "Espresso"
---

<figure class="image">
    <img src="assets/images/2022/05/espresso-part5.png" alt="Espresso logo and the title Hello, espresso! Part 5 Automating WebViews 🕸">
    <figcaption>
        Espresso logo image by <a
            href="https://www.google.com/imgres?imgurl=https%3A%2F%2Fmiro.medium.com%2Fmax%2F600%2F1*Z2iFvuo4pMsK-aYhPkiGWA.png&imgrefurl=https%3A%2F%2Fproandroiddev.com%2Ftesting-android-ui-with-pleasure-e7d795308821&tbnid=2m9PR31uA1zqGM&vet=12ahUKEwjtm9SLnMT3AhVE8IUKHREuDVUQMygAegUIARCpAQ..i&docid=cWI2R5HvetOtGM&w=600&h=692&q=espresso%20android&ved=2ahUKEwjtm9SLnMT3AhVE8IUKHREuDVUQMygAegUIARCpAQ">Pro Android Dev</a> 
    </figcaption>
</figure>

In the last part [Hello, espresso! Part 4 Working with Idling resources
😴]({% link _posts/2022-05-14-hello-espresso-part-4-idling-resources.md %}),

We understood how to use espresso idling resources to achieve synchronization
when the app is running background tasks that espresso is not aware of. Go ahead
and have a read in case you missed it.

## Automating hybrid apps with WebViews

Switching gears to a different topic now, many apps expose certain business
logic in WebViews (a.k.a a mobile browser),

For example a help or support page for your business that needs to be dynamic
and change whenever a new page/option is added or some marketing content is
launched, Or even lengthy terms and conditions for a new feature

In these cases, its important that we have confidence that when the user
interacts with these `WebViews`, the interactions work well

## Resources 📘

- You can find the app and test code for this post on Github:
  - [App](https://github.com/automationhacks/testing-samples/tree/main/ui/espresso/WebBasicSample)
  - [Test code](https://github.com/automationhacks/testing-samples/blob/main/ui/espresso/WebBasicSample/app/src/androidTest/java/com/example/android/testing/espresso/web/BasicSample/WebViewPracticeTest.java)
- Please read
  [Espresso Web](https://developer.android.com/training/testing/espresso/web) on
  android developers for some more context

## Conclusion ✅

Hopefully, this post gives you an idea of how to work with Idling resources in
espresso. Stay tuned for the next post where we’ll dive into how to automate and
work with **WebViews** with espresso

As always, Do share this with your friends or colleagues and if you have
thoughts or feedback, I’d be more than happy to chat over on Twitter or
comments. Until next time. Happy Testing and learning.
