---
id: 449
title: Using TestNG setup/teardowns with data provider combinations
date: 2020-02-22T03:58:01+00:00
author: Gaurav
excerpt: Sometime back, I tried to update my Kotlin test code using TestNG to use data providers and Before/After annotations and it did not work immediately. After some research I found the solution. Here is a post, explaining how to use these constructs well with an example.
layout: post
guid: http://automationhacks.blog/?p=449
permalink: /2020/02/22/using-testng-setup-teardowns-with-data-provider-combinations/
jabber_published:
  - "1582343887"
timeline_notification:
  - "1582343889"
email_notification:
  - "1582343889"
categories:
  - Framework development
  - Kotlin
  - Programming
  - Test frameworks
  - Testng
---
<p class="has-drop-cap">
  Data providers ♥&nbsp;are a super convenient feature to run the same tests with multiple sets of data. I use them quite heavily on a day to day basis in my automated tests and it helps me to write code that adheres to the <a href="https://dzone.com/articles/software-design-principles-dry-and-kiss">DRY</a> principle quite easily.
</p>

I wrote a post on understanding how to use Data providers in TestNG with Kotlin some time back. You can check it out [here](https://automationhacks.blog/2019/09/17/working-with-testng-data-providers-in-kotlin/)

## The case for setup and teardowns via @Before and @After

Another useful feature and common pattern while writing clean tests with TestNG is the use of `@Before` and `@After` annotations at different levels (method, class, suite, etc)

They afford us a couple of unique conveniences and are a sensible pattern to follow:

  * **Before** annotated functions always run before the test/group of tests and if any failure occurs in this section then it is reported as a warning in setup code and not the test method
  * They allow cleaner separation of pre and post-condition logic from the actual test code allowing better readability&nbsp;
  * Methods annotated with **After** always run even if some assertion fails in the test code, Allowing you to gracefully reset any temporary data that might have been created or god forbid modified by a test

## @Before and @After annotations with @Dataprovider

However what if I want to do both setup/teardown for the test based on the data in the data provider combination?



## How do we test this behavior?

Let's come back to our test cases.&nbsp;

We would want to check that a booking can be made successfully for a vehicle type.

Below is a test for the same, We make a booking and then check if the booking exists in the system with simple assertions.

<div class="gist-oembed" data-gist="d7e08b92a3d95f388b51b028f3e22b60.json" data-ts="8">
</div>

Now, this is all fine, but what if we want to test the same flow for multiple different vehicle types? For instance, in this case, **Car and Car XL** vehicle types.

Surely you can copy the same test and replace the vehicle type with Car right?

Well, it would just lead to a maintenance nightmare later on with all the duplicated code.

> By **eliminating the duplicates**, you ensure that the code says everything once and only once, which is the **essence of good design**.
> 
> &#8212; Fowler, Martin. Refactoring (Addison-Wesley Object Technology Series) (pp. 55-56). Pearson Education. Kindle Edition.

## Data providers to the rescue

We could instead use data providers to run the same test with different data. Here is how that would look like.

<div class="gist-oembed" data-gist="7c35352cf2c23b129e007ae96e024f57.json" data-ts="8">
</div>

If we run the test then it would work fine.

<img loading="lazy" class="alignnone size-full wp-image-512" src="https://i2.wp.com/automationhacks.blog/wp-content/uploads/2020/02/testwithdataprovider.png?resize=750%2C103&#038;ssl=1" alt="testWithDataProvider.png" width="750" height="103"  data-recalc-dims="1" /> 

However, we already knew that data providers are awesome and can be used from this previous [post](https://automationhacks.blog/2019/09/17/working-with-testng-data-providers-in-kotlin/)

## Let's expand the problem:

Now that the booking creation test looks fine. What if we want to test the cancellation flow? i.e.

> As a user I should be able to cancel the created booking

Let's add a test for the cancel flow:

The test follows below flow:

  1. Make a booking
  2. Check if the booking is made
  3. Cancel the booking
  4. Check booking is canceled

Now to show, what do most of us immediately tend to do in situations like this?

I copied the code from booking creation and then added the code for the cancellation flow.&nbsp;

<div class="gist-oembed" data-gist="597a1adbbad1b83460cd04cda20b1e3f.json" data-ts="8">
</div>

While this works, this certainly violates the **DRY** principle. We have the same code in two different test methods and added a bunch of more problems for ourselves.

  * What if there is a change in the Booking class? We would now have to make the same change in multiple places.
  * Also, the test methods' size has just gone up to 15 LOC. While this is manageable now. It can quickly turn bad if we do this 10, 20 or 50 times. After that welcome to 2 hours of debugging every morning when something fails and heaven forbid if you have to update these tests.

## Using setup/teardown blocks

If you notice, both the test methods need the booking to be created as a pre-requisite right?

Let's refactor these methods to make use of Setup `@Before`feature of TestNG

Here are the changes I have made:

  * I created a **givenBookingIsCreated&nbsp;**method annotated with **@BeforeMethod&nbsp;**so that it runs for all the tests
  * Extracted **orderId** as a class level property which would be initialized by the setup method (Line 2)
  * Removed the booking creation related code from the test methods

> Side note. I realized that you cannot specify a Kotlin primitive (Int) as lateinit and thus I refactored the booking class to have the **orderId** of type **String**

<div class="gist-oembed" data-gist="8a5defa1f6c49c939570be6ba3b0dd5f.json" data-ts="8">
</div>

The code looks much better now. Let's run it.

## Oops!&nbsp;

In typical developer fashion. The code rarely works the first time. 🙂 Plus we were able to bomb all our tests!&nbsp;

<img loading="lazy" class="alignnone size-full wp-image-514" src="https://i0.wp.com/automationhacks.blog/wp-content/uploads/2020/02/before_method_failure.png?resize=750%2C178&#038;ssl=1" alt="before_method_failure.png" width="750" height="178"  data-recalc-dims="1" /> 

Let's take a look at the exception:

> org.testng.TestNGException:  
> **Can inject only one of <ITestContext, XmlTest, Method, Object[], ITestResult>** into a **@BeforeMethod** annotated givenBookingIsCreated.  
> For more information on native dependency injection please refer to <a href="http://testng.org/doc/documentation-main.html#native-dependency-injection" rel="nofollow">http://testng.org/doc/documentation-main.html#native-dependency-injection</a>

TestNG is such a kind framework to give us all the details that we need to fix this. It mentions that we can only have certain types of dependencies injected into the **@BeforeMethod&nbsp;**which are **<ITestContext, XmlTest, Method, Object[], ITestResult>**

Hmm.

Lets back up a bit.&nbsp;

  * Our original requirement was that we want to set up different types of bookings such that the booking and cancellation test can verify that those flows are working fine
  * We want to use data providers so that we don't have to write the same test for different sets of data.

Turns out the culprit very rightly is that **we thought we could pass around any parameters used in the test method to before method as well**.

<pre>fun givenBookingIsCreated(vehicleType: VehicleType)</pre>

## Let's fix this:

I have replaced the parameter with an **Object[]&nbsp;**which can be represented as **Array<Any>&nbsp;**in kotlin, additionally, we need to extract the param that we care about and cast it to the desired type

<div class="gist-oembed" data-gist="b092015a4c9f89232cd39c6da7403e8f.json" data-ts="8">
</div>

Let's run the tests again:

This is what I was looking for. All tests passed. Time for some well-deserved coffee.

<img loading="lazy" class="alignnone size-full wp-image-516" src="https://i2.wp.com/automationhacks.blog/wp-content/uploads/2020/02/final_test_run.png?resize=750%2C149&#038;ssl=1" alt="final_test_run.png" width="750" height="149"  data-recalc-dims="1" /> 

## Key takeaways:

  * With following this approach of combining **Before/After** annotations with Data provider values, we can keep our test method code leaner
  * TestNG Dependency injection is quite powerful and used correctly gives your amazing powers. Read more about it <a href="https://testng.org/doc/documentation-main.html#dependency-injection" target="_blank" rel="noopener">here</a>
  * Do not repeat yourself while coding, please! 😉
  * You can find the complete Gist with the latest code <a href="https://gist.github.com/gaurav-singh/48c3d1e71edaf5ea429075a1a511e6c1" target="_blank" rel="noopener">here</a>

Hopefully, this long-winded story about TestNG data providers and setup methods gave you something valuable to take away. I recently faced this problem at work and could find this solution.&nbsp;

Are there better ways to solve this? Let me know in the comments and if you found this useful, Do share with a friend or colleague. Until next time! Cheers!