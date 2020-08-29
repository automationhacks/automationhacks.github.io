---
id: 48
title: "Vol 1: How Kotlin eased my life in a Java world"
date: 2019-06-16T12:47:33+00:00
author: Gaurav
layout: post
permalink: /2019/06/16/vol-1-how-kotlin-eased-my-life-in-a-java-world/
categories:
  - Kotlin
  - Programming
---

_Part 1 of a series of posts on why coding in kotlin makes so much sense over
java._<figure class="wp-block-image wp-caption">

<img src="https://i0.wp.com/automationhacks.blog/wp-content/uploads/2019/06/c11a8-1vapfvieh667oaspz5f3noq.png?w=750&#038;ssl=1" alt="" data-recalc-dims="1" />
<figcaption>A Kotlin&nbsp;function</figcaption></figure>

Hello wonderful people,

<blockquote class="wp-block-quote">
  <p>
    Over my 8 years of experience as a coder/Quality engineer the language which gave me the comfort of feeling at home <em>was and still is</em> “<strong>Python</strong>” 🐍 till&nbsp;date.
  </p>
</blockquote>

It allowed me to truly solidify concepts in programming as well as gave me the freedom to write
concise code quickly to turn my ideas into executable logic and it was a ton of fun.

The dynamic nature/duck typing, No worries about types, use of higher order functions and focus on
<a href="https://www.python.org/dev/peps/pep-0020/" target="_blank">writing readable and explicit
code</a> while solving problems was something which i really adore in the language.

When I switched jobs a year back. Most of the test automation code in my new company was written in
Java. And even though I quickly started learning and became fluent in the language, Java and its
constructs felt too verbose and syntax heavy to me. I found myself spending more time worrying about
types all the time rather than actually getting code out and though i was productive with it in a
short amount of time. **It never felt ease like Python**.

<blockquote class="wp-block-quote">
  <p>
    Until i discovered Kotlin close to 3 months back. And this is the story of how Kotlin changed my life in a world full of Java code.&nbsp;🙂
  </p>
</blockquote>

With that pretext. Let’s dig into what are some of the features of Kotlin language which simplify
our life as a programmer in the JVM world.

In researching for this post, I went through multiple blogs and most of these examples are from a
<a href="https://www.youtube.com/watch?v=6P20npkvcb8" target="_blank">talk</a> given at Google IO by
none other than the lead kotlin language designer
<a href="https://twitter.com/abreslav?lang=en" target="_blank">Andrey Breslav</a> 🙌

### Classes

#### **1.1 Concise classes with automatic Getters and&nbsp;Setters**

One of the trademark constructs in Java is a bean/POJO which on a high level is primarily a bunch of
Getters/Setters and constructors to represent an object.

Let’s say we wanted to represent a Person having a name and age. Below is how we would write this in
Java.

{% gist 870cbe3cbf91927ab46935a52ebc7bf6 %}

And here is the equivalent code in Kotlin: 😆

{% gist f9090a01fb8cd9e6a05b3ce26d0bc118 %}

Kotlin allows us to define name and age as properties in the constructor itself with automatic
getters and setters generated. Pretty slick right?

Also Kotlin allows to directly access the properties via their name. Avoiding the whole
getProperty() or setProperty() syntax. So much less clutter.

{% gist 7067edd21b02d8d61b479e28afd59275 %}

#### 1.2 Data Classes are cheap and&nbsp;concise

Classes in Kotlin are cheap to create and can be created in any&nbsp;.kt file without requiring the
File name to match the class name itself and we have a modifier called as `data` which unlocks so
much additional features out of the box.

Let’s see an example of this:

{% gist 602fa2e1dad405cacfb1ff518b11ed6c %}

Let’s examine the above code:

- parseName is a function that takes a full name and returns a list of separated first and last
  names
- In main function we are unpacking them and asserting if the function did its job correctly.

<blockquote class="wp-block-quote">
  <p>
    <strong>Another cool feature to note:</strong> Kotlin has string interpolation so we can directly refer to variables inside a string using <code>$</code> symbol like <code>println("$first $last")</code>
  </p>
</blockquote>

The above code is quite ugly since we are abusing a list to store and return the result and using
the weird slicing syntax to get elements.

We can quickly refactor this code and replace list with a class with 2 properties. With that, we
could quite easily use `dot` to access first name and last name.

{% gist 405294314f01550fa6b155acabf82da1 %}

Sweet, the code is already cleaner. However if we run this code we observe below output.

<pre class="wp-block-preformatted">Jane Doe<br />Equals does not work...</pre>

<pre class="wp-block-preformatted">Process finished with exit code 0</pre>

However we that the two objects are not equal. In Java to make this work we would have to override
and create `equals(), hashCode()`and other convenience methods.

In Kotlin we can directly use data classes which generates the above methods and other convenience
functions for us.

<pre class="wp-block-preformatted">data class FullName<em>(</em>val first: String,<br />               val last: String<em>)</em></pre>

If we were to run the same code again this would work just fine.

### Functions

#### 1.1 Functions are first class&nbsp;citizens

Kotlin like many modern languages treats functions as a first class citizen. Meaning functions **do
not need an enclosing class.**

Lets understand this with an example.

Below is a simple StringUtils class having some convenience methods to get the first word in a
string.

This is similar to how we would write this code in Java. Though this is definitely not idiomatic.

{% gist 5180077b86ca19d61b0bc68550608e42 %}

Surely we can do better here.

Turns out we can, Observe the below code for a second. We obviously moved the functions outside the
class and removed StringUtils class itself which was obvious but where is the overloaded
`getFirstWord` method?

<blockquote class="wp-block-quote">
  <p>
    Turns out Kotlin supports default parameters and so we could always give separator a default value of <code>" "</code> and avoid having to write multiple overloads and the code already looks so much&nbsp;concise.
  </p>
</blockquote>

{% gist 183ceedb143a30faa476e2a61f742047 %}

Obviously i could always pass specific separator value as needed using the named parameter syntax as
below:

<pre class="wp-block-preformatted">val first = getFirstWord("Jane,Doe", separator = ",")</pre>

#### 1.2 Extension functions

Wouldn’t the above code read so much nicer if we were able to something like below:

<pre class="wp-block-preformatted">"Jane Doe".getFirstWord()</pre>

Turns out Kotlin provides a special construct to **extend** the functionality of a class using
functions called extension functions.

All we did is provided the class which we want to extend, in this case `String` followed by the
function name, Since we are working off a string we could remove the `word` param and instead just
refer to the string using `this` and voila! with this we could achieve our objective and attach new
functionality to an existing class which might not be in our control (In this case the Standard
String class)

{% gist 079cb645eda698f3e87c1358a98ede00 %}

Kotlin also supports extension properties.

How do we do this?

Essentially what we can do is define a new property on String class like
`val String.lastWord&nbsp;: String` and then define a get() which returns us the required value.

<pre class="wp-block-preformatted">val String.lastWord : String<br /><br />get() {<br />    return this.split("")[1]<br />}</pre>

We can use this just like a normal property with a clean syntax like `"John Doe".lastWord`

<pre class="wp-block-preformatted">fun main() {<br />    val last = "John Doe".lastWord<br />    println("Last word (Using extension properties) $last")<br />}</pre>

Here is the final code with all the above changes made:

{% gist e40512afdd071f0d04cacfc8f457c7b4 %}

#### 1.3 Inner functions

Kotlin supports local functions without any other ceremony around it. Lets dig into this with an
example.

Generally when working with data whether it be in JSON/YAML format we typically might need to use
recursion to walk through in the hierarchy.

In the below code:

We have a simple `Element` base class and a `Container` class which can wrap multiple Element
objects. Also we have a `Text` class which inherits from Element and holds a text.

If we want to extract texts from all the leaf nodes, then we need to write a function as
`extractText` which takes an element and then either adds it’s text to a `StringBuilder` object or
if it’s a container type then it recurses till it has walked through all elements.

{% gist 4d5a671d069f4c5e3aa0cf237d76a7c4 %}

This looks good right? We are using **top level functions,** however we can improve this code a lot.

If you observe `extractFunction()`function is only being used inside the extension function on
`Element` so its a good candidate to make it local.

Let's move it as a local or inner function and also move out `StringBuilder` and make it a local
variable.

{% gist 749a37e569b83e47d8470bdcf3fbf9c1 %}

Sweet.

We can take this a bit further, We can inline `val text = e` since we are just assigning the
variable to text and using it. Also we can convert this `if else` statements into a `when` statement
which is more nicer and provides a useful `is` clause.

Let’s see how it looks like when these refactorings are performed.

{% gist b61391d486919d9f3ccf8cfe3dd018aa %}

This is so much more intuitive than the noisy `if else` chain of statements.

Can we improve something more on this?

Turns out we can.

<pre class="wp-block-preformatted">for (child in e.children) {<br />                extractText(child)<br />            }</pre>

We need to iterate in all elements and then recursively call the function right. This could be very
easily replaced with below:

<pre class="wp-block-preformatted">e.children.forEach(::extractText)</pre>

The overall function looks like below. We have already made this so much simpler.

{% gist 4a8bcec0ae180affea3a71cf99d31461 %}

However if you see there is an annoying `else` clause in the when statement. Since we know exactly
how many classes inherit from Element, we can improve this by making the `Element` class as `sealed`

<pre class="wp-block-preformatted">sealed class Element</pre>

And now we can get rid of the else clause since we know that `Element` subclasses are known

The final code looks like below:

Just by applying idioms of Kotlin language we have been able to reduce the code complexity and
increase readability at the same time.

{% gist 26055966af32c70d36e068a74ce42aa1 %}

And that’s it for this post.

I would talk about other cool features in a future post as well as how I implemented these in my own
api tests. Stay tuned.

If you find this article useful or informative in any way, why not share it with a friend or
colleague.

See you all in the 2nd part of this series! Until then, Happy testing and coding! Cheers! ☮️
