---
id: 991
title: How to write a generic wait function in Kotlin
date: 2020-08-08T03:26:30+00:00
author: Gaurav
layout: post
guid: http://automationhacks.blog/?p=991
permalink: /?p=991
categories:
  - Uncategorized
---
In Test automation, one of the most common scenarios that we need to handle is **X is not ready** and we need to **wait for X to be ready** and in a state where we can proceed. 

Having a test that does not waiting for slow resources to be in a state where we can work with it just causes tests to be flaky. Sometimes the resource is ready and our test passes but most of the times it fails. This is just an excercise in frustration

Some of the common use cases could be:

  * A business API that needs approx 5 seconds to show a transaction
  * A flaky third party API that might return a 500 occasionally but is usually up within a few seconds

## Let&#8217;s wait. 🤷🏻‍♂️

What are some of the ways we can work around this:

### Hardcoded sleep

You could put a `Thread.sleep()` before you try the operation. That would work, but we would unnecessarily wait till `x` seconds every time we run this case. 

What if you run this case for a data combination of 100 rows. Your **10** seconds hardcoded wait could quickly become **~16 mins**. Yikes! 

### Explicit Wait

A quite popular concept in Selenium is to use an `ExplicitWait`, wherein you make the test wait until an expected condition evaluates to `True` or a timeout is hit, whichever is earlier.

This is an ideal way to handle a situation like this. However what if we are not using Selenium or even automating a UI?

## A generic wait function ⏰

I face this problem so commonly that I decided to write a generic wait function in Kotlin which I can use easily whenever I faced a situation like this