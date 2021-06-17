---
title: Working with TestNG data providers in Kotlin
excerpt: "Data providers are not new, they are a cool feature in TestNG, in this post, we see how to implement these in Kotlin language"
permalink: /2019/09/17/working-with-testng-data-providers-in-kotlin/
categories:
  - Coding
  - "Test automation"
tags:
  - Kotlin
  - TestNG
---

![](/assets/images/wp-content/uploads/2019/09/juan-gomez-kt-wa0gdfq8-unsplash.jpg)

Photo on [Unsplash](https://unsplash.com/search/photos/keyboard?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) by Juan Gomez

Hello there,

TestNG needs no introduction, It is one of the more popular test frameworks available in Java/JVM
ecosystem and offers many advanced features like running tests in parallel, flexible annotations to
do setups and teardowns at different levels and group tests and run them selectively.

One of the more useful features in TestNG are `Data Providers` which can be used to pass multiple
variations of data to the same test method and have TestNG automatically generate tests

This saves the test author so much of time while avoiding him/her the effort of writing duplicated
code with just the data being different.

When I switched to using Kotlin to write my tests in, I decided to use TestNG as the framework of
choice. However, the implementation of data providers was a tricky problem in the beginning.
Hopefully this post saves you that time.

## A simple problem with data providers:

Let's assume that you want to write tests for a simple method `add()`in a `Calculator` class which
takes 2 nos, adds them up and verifies the result is equal to an expected value.

Below code represents the `Calculator` class.

{% gist b513548ff03e7002160091570a047be1 %}

Let's see a basic test for this class:

{% gist e3967cb8ed9b18fba899ea861b606e1a %}

The above test works and passes. What if we want to test if our calculator is able to perform
addition operation for multiple different sets of data. Well that's where a data provider comes in
picture.

{% gist ca161826f3df02319a4fe777bf28807b %}

As per TestNG docs:

<blockquote class="wp-block-quote">
  <p>
    @DataProvider : <strong>Marks a method as supplying data for a test method. The annotated method must return an Object[][] where each Object[] can be assigned the parameter list of the test method. The @Test method that wants to receive data from this DataProvider needs to use a dataProvider name equals to the name of this annotation.</strong>
  </p>
  
  <cite><a href="https://testng.org/doc/documentation-main.html">https://testng.org/doc/documentation-main.html</a></cite>
</blockquote>

Couple of things to note:

1. Kotlin `Any` is equivalent to `Object`
2. We need to pass an array nested inside another array such that each nested array acts as a row of
   data for the test method
3. Thus for above example, we create a variable `testData` of type `ArrayList<Array<Int>>` to hold
   this required data. Note: _Int could be any primitive or complex data type (for instance even
   objects of a required type)_
4. We add the required rows of data as `arrays of Int` and keep on adding it to `testData` arrayList
5. Finally, It's important to return a `MutableIterator` of these arrays in order for this to work.
   We can get this by applying `.iterator()` method on the arrayList.

Now when we run this test, we observe below tests are generated in
IntelliJ.

![Test runner](/assets/images/wp-content/uploads/2019/09/image.png)

Awesome. The same pattern can be repeated for any required data provider.

## Abstracting data providers

So what if we have a set of data providers which are used by many test classes and we want to
abstract this detail away from the Test class.

Below are some rules which are used for discovering data providers by TestNG:

<blockquote class="wp-block-quote">
  <p>
    By default, the data provider will be looked for in the <strong>current test class</strong> or one of its <strong>base classes</strong>.
  </p>
  
  <cite>TestNG docs</cite>
</blockquote>

Cool. Let's see an example of this.

Let's assume we want to use the same data provider for a new `sub()` method of calculator class
which subtracts the two nos.

We can define a new `CalculatorBaseTest` class (remember to mark it with `open` keyword to allow it
to be extended) and move this method there and ensure that our `CalculatorTests` inherits from this
class as below:

`class CalculatorTests : CalculatorBaseTest()`

Here is the complete base class.

{% gist 5c933f38e2371b9b3bd21c7442847434 %}

Here is the updated `Calculator` class with the `sub()` method

{% gist 57ba0d23d667f0e15bf39fa8665b8494 %}

And the updated Test class:

{% gist cadfca888c613dcee28bdbe2a62cec61 %}

## Moving data providers in a dedicated class

What if we don't want to create an inheritance hierarchy and want all the related data providers to
be in a single file. Turns out this can also be achieved easily in Kotlin.

As per docs:

<blockquote class="wp-block-quote">
  <p>
    <em>If you want to put your data provider in a different class, it needs to be a static method or a class with a non-arg constructor, and you specify the class where it can be found in the&nbsp;dataProviderClass&nbsp;attribute:</em>
  </p>
</blockquote>

In Kotlin, static methods are defined using `companion object` inside classes. However if we try
with just putting the data provider method inside and try, it does not work and the Tests are
ignored. After a bit of Googling, I figured out that you also need to annotate the method with
`@JvmStatic` to ensure this works.

Here is the standalone file with the data provider in it:

{% gist d8c8162d492dada4eea6aa4be096d745 %}

And the test method which picks up the values from the above specified data provider, Note: The
`@Test` annotation needs a argument `dataProviderClass` to be passed with a reference of `KClass`
and thus it needs to be `<NameOfTheClass>::class`

{% gist 70e50e52d9248f0b31a735da4aed818c %}

With this, we can organize our data providers in desired files.

## Sequential is so boring. Let's parallelize:

With all the above examples, TestNG would execute all the generated test methods in a single thread
and depending on how much time each method takes, this can greatly increase your test execution
time.

Turns out this is so trivial to setup that you would greatly appreciate how wonderful TestNG is as a
framework.

We need to do below steps:

1. Add `parallel = true` in the `@DataProvider` annotated method
2. Optionally add `threadPoolSize` to specify the no of threads that should be used to execute the
   tests in `@Test` annotation.

Here is the updated BaseTest method:

{% gist a857f1faf2c25da07b99e42043eaf5fc %}

And the updated Test:

{% gist 7d791338a13618bdb8a1fda6d9503647 %}

This small change can greatly add parallel super powers to your tests. However do ensure you use
this carefully. Multithreading and concurrency are niche topics in itself and it helps to understand
how the nuts and bolts work to ensure you avoid yourself some debugging pain. More on this in a
future post.

And that's it for this post folks. If you found this useful, Do share it with your friends and
colleagues and I would like to hear in the comments in case you have suggestions.
