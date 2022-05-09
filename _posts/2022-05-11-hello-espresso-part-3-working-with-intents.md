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

## What is an intent?

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

## Understand App under test

Let's start by understanding the app under test

We'll use
[`IntentsBasicSample`](https://github.com/automationhacks/testing-samples/tree/main/ui/espresso/IntentsBasicSample)
app, which has an `EditText` to enter a phone no and a `Button` to either call a
number or to randomly pick a no.

The below scenarios are possible

> I've written this in Gherkin syntax for clarity, however in a live test, the
> tests should always describe behavior and no be as procedural as i've written
> below. Read [this](https://cucumber.io/docs/bdd/better-gherkin/) page on
> cucumber website to understand more

Let's use Layout inspector to grab the selectors for the elements we want to
work with:

![Layout inspector](../assets/images/2022/05/intents-layout-inspector.png)

```text
GIVEN user is on home screen
WHEN user taps on enter phone no EditText with id: @id/edit_text_caller_number
AND user taps on call number Button with id: id	@id/button_call_number
THEN the dialer activity is shown with entered phone no
```

```text
GIVEN user is on home screen
WHEN user taps on pick number Button with id: @id/button_pick_contact
AND user taps on call number Button with id: @id/button_call_number
THEN the dialer activity is shown with entered phone no
```

![Intents basic sample home](../assets/images/2022/05/intents-home-with-no.png)

![After user tapped on call number](../assets/images/2022/05/intents-dialer.png)

## Let's automate these intents

### Add dependencies

We need to add `espresso-intents` dependency to our `app/build.gradle` file as
below, also its only compatible with espresso `2.1+` and android testing lib
version `0.3+`, so we double check these versions

```java
androidTestImplementation 'androidx.test.espresso:espresso-intents:3.4.0'
androidTestImplementation 'androidx.test:runner :1.4.0'
androidTestImplementation 'androidx.test:rules:1.4.0'
androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
```

### Setting up intents and permissions

Below is the complete test to perform our scenario, don't worry if it does not
make sense right now, we'll unpack this in further sections

```java
@RunWith(AndroidJUnit4.class)
@LargeTest
public class DialerActivityPracticeTest {
  public static final String VALID_PHONE_NUMBER = "123-456-7898";

  @Rule
  public GrantPermissionRule grantPermissionRule =
      GrantPermissionRule.grant("android.permission.CALL_PHONE");

  @Rule
  public IntentsTestRule<DialerActivity> testRule = new IntentsTestRule<>(DialerActivity.class);

  /** Test to enter a phone number and make a call and verify an intent is launched */
  @Test
  public void whenTapOnCallNumber_ThenOutgoingCallIsMade() {
    // Type a phone no and close keyboard
    Uri phoneNumber = Uri.parse("tel:" + VALID_PHONE_NUMBER);
    onView(withId(R.id.edit_text_caller_number)).perform(typeText(VALID_PHONE_NUMBER), closeSoftKeyboard());

    // Tap on call number button
    onView(withId(R.id.button_call_number)).perform(click());

    // Verify an intent is called with action and phone no and package
    intended(allOf(hasAction(Intent.ACTION_CALL), hasData(phoneNumber)));
  }
}
```

- Just like `Views`, we'll use JUnit rules to setup and teardown our intents
  before and after each test. We use `IntentsTestRule` for this instead of
  `ActivityTestRule`.
- Since we want to automate the `DialerActivity` class, we'll pass that as the
  type

```java
@Rule
public IntentsTestRule<DialerActivity> testRule = new IntentsTestRule<>(DialerActivity.class);
```

- We also want our test to have permissions to make a call and thus add below
  snippet as another JUnit rule to ensure we don't get any permission errors

```java
@Rule
public GrantPermissionRule grantPermissionRule = GrantPermissionRule.grant("android.permission.CALL_PHONE");
```

With that taken care of lets write our test

We store a test number in a static variable

```java
public static final String VALID_PHONE_NUMBER = "123-456-7898";
```

We'll type the phone no into our EditText as below and then close the keyboard:

```java
onView(withId(R.id.edit_text_caller_number)).perform(typeText(VALID_PHONE_NUMBER), closeSoftKeyboard());
```

We'll then tap the call number button

```java
// Tap on call number button
onView(withId(R.id.button_call_number)).perform(click());
```

Great, we want to verify that our Intent was actually invoked and we can achieve
that using `intented` method that takes an Intent matcher (either an existing
one or our own). Referring to
[Hamcrest Tutorial](https://code.google.com/archive/p/hamcrest/wikis/Tutorial.wiki)
is also a resource you can consider to become more comfortable with writing
matchers

```java
// Verify an intent is called with action and phone no and package
intended(allOf(hasAction(Intent.ACTION_CALL), hasData(phoneNumber)));
```

- If you notice, we use `allOf()` matcher, that checks that the examined object
matches **all of the specified matchers**
- We then check that the `intent`
