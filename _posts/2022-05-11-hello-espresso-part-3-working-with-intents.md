---
title: Hello, espresso! Part 3 Working with intents
excerpt:
  "Learn how to automate android intents (with and without stubbing) using
  espresso"
permalink: 2022-05-11-hello-espresso-part-3-working-with-intents
published: false
image: /assets/images/2022/05/espresso-part3.png
canonical_url: ""
categories:
  - android
  - espresso
  - ui-automation
  - mobile
tags:
  - "Mobile Testing"
  - "Android Testing"
  - "Espresso"
  - "Software Engineering"
---

<figure class="image">
    <img src="assets/images/2022/05/espresso-part3.png" alt="Espresso logo and the title Hello, espresso! Part 3 Working with intents">
    <figcaption>
        Photo by <a
            href="https://www.google.com/imgres?imgurl=https%3A%2F%2Fmiro.medium.com%2Fmax%2F600%2F1*Z2iFvuo4pMsK-aYhPkiGWA.png&imgrefurl=https%3A%2F%2Fproandroiddev.com%2Ftesting-android-ui-with-pleasure-e7d795308821&tbnid=2m9PR31uA1zqGM&vet=12ahUKEwjtm9SLnMT3AhVE8IUKHREuDVUQMygAegUIARCpAQ..i&docid=cWI2R5HvetOtGM&w=600&h=692&q=espresso%20android&ved=2ahUKEwjtm9SLnMT3AhVE8IUKHREuDVUQMygAegUIARCpAQ">Pro Android Dev</a> 
    </figcaption>
</figure>

Things are getting pretty exciting, in the previous part [Hello, espresso! Part
2 Working with
lists]({% link _posts/2022-05-07-hello-espresso-part-2-working-with-lists.md %}),
we learnt how to work with list controls (`RecyclerView`, `AdapterView`) in
espresso. Go ahead and have a read in case you missed it.

## Learning to test Intents

In this post, we'll understand how to automate testing of intents using
espresso.

`espresso-intents` provides us the capabilities to validate whether the correct
intent is invoked with valid data by our app or even stub out the intents sent
out so that we can verify only our apps logic (while assuming other app that we
depend upon has been tested independently)

### What is an intent?

In
[developer.android.com's post of Intent](https://developer.android.com/reference/android/content/Intent)

> An intent is an abstract description of an operation to be performed.
>
> It can be used:
>
> - with `startActivity` to launch an Activity,
> - `broadcastIntent` to send it to any interested `BroadcastReceiver`
>   components,
> - and `Context.startService(Intent)` or
>   `Context.bindService(Intent, ServiceConnection, int)` to communicate with a
>   background Service.

One of the use cases for which **Intents** are used a lot is to **launch
Activities** and they can be thought is a data structure that holds an abstract
description of an action to be performed

There are 2 components to an Intent:

- **Action:** What action has to be performed, for example:
  - [`ACTION_VIEW`](https://developer.android.com/reference/android/content/Intent#ACTION_VIEW)
    displays data to the user, for instance, if we use it as `tel: URI` it will
    invoke the dialer (we'll see this in our example),
  - [`ACTION_EDIT`](https://developer.android.com/reference/android/content/Intent#ACTION_EDIT)
    gives explicit edit access to given data
- **Data:** Data to operate on expressed as a
  [`Uri`](https://developer.android.com/reference/android/net/Uri)

You can read the full doc
[here](https://developer.android.com/reference/android/content/Intent) to
understand Intents in depth

### Understand App under test

Let's start by understanding the app we are testing and the flow we want to
automate.

We'll use
