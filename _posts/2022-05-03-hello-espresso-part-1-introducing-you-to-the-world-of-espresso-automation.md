---
title:
  Hello, espresso! Part 1 Introducing you to the world of espresso automation!
excerpt: "Getting started with Android automation using Espresso"
permalink: 2022-05-03-hello-espresso-part-1-introducing-you-to-the-world-of-espresso-automation
published: true
image: /assets/images/2022/05/espresso-part1.png
canonical_url: "https://automationhacks.substack.com/p/hello-espresso-part-1-introducing?s=w"
categories:
  - android
  - espresso
  - ui_automation
  - mobile
tags:
  - "Mobile"
  - "Testing"
  - "Android Automation"
  - "Espresso"
  - "Software Engineering"
---

<figure class="image">
    <img src="assets/images/2022/05/espresso-part1.png" alt="Espresso logo and the title Hello, espresso! Part 1 Introducing you to the world of espresso automation!">
    <figcaption>
        Espresso logo by <a
            href="https://www.google.com/imgres?imgurl=https%3A%2F%2Fmiro.medium.com%2Fmax%2F600%2F1*Z2iFvuo4pMsK-aYhPkiGWA.png&imgrefurl=https%3A%2F%2Fproandroiddev.com%2Ftesting-android-ui-with-pleasure-e7d795308821&tbnid=2m9PR31uA1zqGM&vet=12ahUKEwjtm9SLnMT3AhVE8IUKHREuDVUQMygAegUIARCpAQ..i&docid=cWI2R5HvetOtGM&w=600&h=692&q=espresso%20android&ved=2ahUKEwjtm9SLnMT3AhVE8IUKHREuDVUQMygAegUIARCpAQ">Pro Android Dev</a> 
    </figcaption>
</figure>

Espresso is a UI automation library for Android maintained by Google and has
become the defacto standard to write android UI tests. The core API is concise
and simple however sometimes wrapping your head around its nitty-gritties could
prove to be a challenge if you don’t live and breathe android day in and day
out.

With this series, I’m hoping to change that. We’ll approach espresso from the
perspective of an n00b engineer (I.e. a beginner trying to get familiar and most
importantly start) and try to deconstruct what it means to write effective and
scalable Android UI automation.

We have lots of interesting capabilities to explore and I’m super excited to
start this journey along with you.

Let’s start, shall we?

## Why espresso?

If you’ve had previous experience with E2E Automation with Appium or other
tools, you may be asking why we should bother to learn a new automation API?

Why not just use Appium espresso driver and use a well-learned API (compatible
with Selenium Webdriver W3C spec nonetheless)?

And you certainly have a point. In **certain contexts**, Appium is a great tool.

However, one of the biggest reasons to prefer Espresso is a combination of
technical and human factors, some of these are listed below:

- **Tests under app codebase:** The tests are written within your app codebase
  and have dedicated tooling support within Android studio, the IDE that android
  devs use day in and day out. This goes a long way in reducing the inertia and
  friction that you may face if you try to onboard devs to write functional E2E
  tests in another repo. I’ve tried this in the past and it's not always the
  most intuitive Dev workflow.
- **Dev don’t need to learn a new language:** You can write tests in Kotlin or
  Java, the language android devs are already familiar with and they don’t have
  to pick up a new language, thus there is less friction in getting devs to
  write tests. In Agile teams with horribly skewed Test to Dev ratios, this
  could be the difference in encouraging a whole team approach to quality.
- **Both black and white box tests:** Espresso supports writing black-box UI
  automation but also has white box access to android code and thus offers a lot
  of power in the hands of the test author since they can leverage knowing
  source code internals to write better and targeted tests.
- **Access to Instrumentation:** Tests have access to instrumentation from
  android and espresso does a lot of synchronization checks behind the scenes
  like checking the message queue is empty and there is no background Async
  processing happening. This is great since you can skip ineffective polling
  logic and let espresso take care of it.
- **Community support:** It’s maintained by Google thus you can be sure of
  dedicated communicated support and enhancements and bug fixes making their way
  into future versions.
- And many more … We can go on and on.

Hopefully, you get the drift and see the possibilities, and are excited to learn
it with me.

> **Talk is cheap, show me the code!**

I’m glad you are as eager as me. Let’s start

## Setting up

We’ll use Android Studio as our main IDE (Integrated development environment).
You can download it from
[Google’s website](https://developer.android.com/studio) and install it on your
machine and platform following the instructions on the site.

We would use example apps already provided by Google engineers in their
open-source GitHub repo
**[testing-samples](https://github.com/automationhacks/testing-samples)** repo
under android.

We will use a forked version of this repo to ensure the codebase does not change
much, however feel free to fork your own version if it helps.

These examples are well written with an app and example espresso tests that
we’ll draw inspiration from to understand espresso API.

For our first example we’ll use
[BasicSample](https://github.com/automationhacks/testing-samples/tree/main/ui/espresso/BasicSample)
repo.

![Basic Sample App](/assets/images/2022/05/basic-sample-1.png)

### Setting up dependencies

We’ll need to add the below dependencies to our **build.gradle** file.

Remember we’ll use the **app/build.gradle** file and not the root level file

```groovy
androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
androidTestImplementation 'androidx.test:runner:1.4.0'
androidTestImplementation 'androidx.test:rules:1.4.0'
```

Also, we’ll set up the test instrumentation runner as `AndroidJUnitRunner` by
adding the below code under `defaultConfig`

```gradle
plugins {
  id 'com.android.application'
}

android {
    compileSdkVersion 28

    defaultConfig {
        applicationId "com.my.awesome.app"
        minSdkVersion 15
        targetSdkVersion 28
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
}

dependencies {
    androidTestImplementation 'androidx.test:runner:1.4.0'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
}
```

After adding this, remember to sync the Gradle project in Android studio to
ensure the above dependencies are downloaded.

## Writing your first android espresso test

For our first hello world test, we’ll open an app screen, perform some UI
actions like type and click and then verify if the app is in the desired state
with an assertion.

Before we write our first test, lets understand basic component of any espresso
test.

### A simple test structure

An espresso test at its heart has 3 main components.

Most of these are imported as static methods.

- **Matcher** - Write a matcher expression that would find an android element.
  For e.g. Find a **View** (ListView, RecyclerView, or DataAdapter).
  - Android espresso uses [Hamcrest matchers](http://hamcrest.org/) expressions
    to specify this. If you are not familiar with Hamcrest matchers, don’t worry
    we’ll understand them more when we look at writing tests.
- **Action** - Once you find an element, you’ll naturally want to perform some
  UI action on it like a real user would
  - You could imagine as a user you may want to:
    - Tap on an element or
    - Type some text or
    - Swipe in any allowed direction and so on …
  - Depending on the element Espresso will provide you with methods to specify
    these actions
- **Assertion** - Great we found an element and also did an action. Are we done?
  Not quite. After performing an action, you should assert if the app actually
  did what you expected it to since a test that does not assert an outcome might
  give a false positive and miss bugs. Espresso provides **Assertion** objects
  depending on the type of element for this.

If you take a step back, this resembles very closely to the
**arrange-act-assert** pattern of writing clean tests. Espresso devs sure did a
good job in implementing this neat pattern right into the core API design.

### Our first test

With those basics and theories out of the way, we are ready to write our first
test.

Let’s understand the flow we want to automate and try it manually first:

1. Open our app under test
2. Launch the MainActivity
3. Find a view with id **editTextUserInput**
4. Type some text into the above edit text box
5. Close keyboard
6. Find a view with id **changeTextBt**
7. Click on the above button
8. Verify the label with id **textToBeChanged** shows the text that we entered

![Basic Sample App](/assets/images/2022/05/basic-sample-2.png)

Here is the
[complete test](https://github.com/automationhacks/testing-samples/blob/main/ui/espresso/BasicSample/app/src/androidTest/java/com/example/android/testing/espresso/BasicSample/ChangeTextBehaviorTest.java):

```java
@RunWith(AndroidJUnit4.class)
@LargeTest
public class ChangeTextBehaviorTest {

    public static final String STRING_TO_BE_TYPED = "Espresso";

    /**
     * Use {@link ActivityScenarioRule} to create and launch the activity under test, and close it
     * after test completes. This is a replacement for {@link androidx.test.rule.ActivityTestRule}.
     */
    @Rule public ActivityScenarioRule<MainActivity> activityScenarioRule
            = new ActivityScenarioRule<>(MainActivity.class);

    @Test
    public void changeText_sameActivity() {
        // Type text and then press the button.
        onView(withId(R.id.editTextUserInput))
                .perform(typeText(STRING_TO_BE_TYPED), closeSoftKeyboard());
        onView(withId(R.id.changeTextBt)).perform(click());

        // Check that the text was changed.
        onView(withId(R.id.textToBeChanged)).check(matches(withText(STRING_TO_BE_TYPED)));
    }
}
```

Let’s unpack this:

#### JUnit annotation

To run any test we use JUnit4 and as such annotate the test class with:

```java
@RunWith(AndroidJUnit4.class)
```

#### Optional test size annotation

Google uses annotations to differentiate between different types of tests and UI
tests are considered as Large tests (since E2E tests are higher fidelity and
take time to run). Simon Stewart (Creator of Selenium Webdriver wrote an
excellent blog on this that is worth a read
[here](https://testing.googleblog.com/2010/12/test-sizes.html))

```java
@LargeTest
```

#### Define JUnit rule

Every espresso test starts by starting an Activity (or a screen) that we want to
test and this is achieved by defining a JUnit rule like below:

```java
@Rule public ActivityScenarioRule<MainActivity> activityScenarioRule
            = new ActivityScenarioRule<>(MainActivity.class);
```

If we see this project this only has a single `MainActivity` and thus we pass
that to `ActivityScenarioRule` class and annotate this with `@Rule`

#### Find an element and perform an action

Now for the fun part, we want to find our textbox, enter some text into it and
then close the keyboard. Let’s see how this is done in Espresso.

```java
onView(withId(R.id.editTextUserInput)).perform(typeText(STRING_TO_BE_TYPED), closeSoftKeyboard());
```

- We start with defining that we are interested in finding a View using
  `**onView()**` method.
- We then say that we want to find the element using **id** using `withId()` and
  pass it the relevant id, in this case `R.id.editTextUserInput`, This returns
  an object of type `ViewInteraction` and we are ready to perform some action on
  this
- In this example we want to type some text, we wrap these actions inside:
  `perform()` method that (if we look at its signature) takes a list of actions
  to be performed in sequence

```java
public ViewInteraction perform(final ViewAction... viewActions) {
```

We can type using: `typeText()` and pass it a string to type on the keyboard

```java
perform(typeText(STRING_TO_BE_TYPED), closeSoftKeyboard());
```

And also pass `closeSoftKeyboard()` to close the keyboard once done.

In similar style, we can click a button by first finding the button and then
performing a tap as below:

```java
onView(withId(R.id.changeTextBt)).perform(click());
```

Finally, as we mentioned a test is incomplete without an assertion.

We’ll check that the text box changes its text based on what we had previously
typed using:

```java
onView(withId(R.id.textToBeChanged)).check(matches(withText(STRING_TO_BE_TYPED)));
```

You can see we find the element using `onView()` and then use the `check()`
method that takes a **ViewAssertion** object judging from its signature and
returns a `ViewInteraction` to chain further methods in sequence if needed

```java
public ViewInteraction check(final ViewAssertion viewAssert) {
```

we specify we want to find check that the element has a text matching what we
entered using `matches(withText(STRING_TO_BE_TYPED))` and this is a familiar
pattern towards writing espresso tests.

## Bonus: Cheat sheet

While the above test is a simple example of the most common app actions that we
could perform, espresso has a rich API capable of supporting different use
cases. We’ll see more of them in subsequent parts of this series. However if you
want to glance at the core API, Google devs have provided a friendly cheat sheet
that you could view
[here](https://developer.android.com/training/testing/espresso/cheat-sheet)

## Conclusion

Hopefully this post gives you an idea on how easy it is to get started with
espresso. Stay tuned for next post where we’ll dive into how to automate
**lists** with espresso

As always, Do share this with your friends or colleagues and if you have
thoughts or feedback, I’d be more than happy to chat over at twitter or
comments. Until next time. Happy Testing and coding.
