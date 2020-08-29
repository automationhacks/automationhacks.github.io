---
id: 112
title: "Vol 2: How Kotlin eased my life in a Java world"
date: 2019-07-12T15:19:46+00:00
author: Gaurav
layout: post
guid: http://automationhacks.blog/?p=112
permalink: /2019/07/12/vol-2-how-kotlin-eased-my-life-in-a-java-world/
jabber_published:
  - "1562944788"
publicize_twitter_user:
  - __gaurav_singh
publicize_linkedin_url:
  - null
timeline_notification:
  - "1562944791"
categories:
  - Kotlin
  - Programming
---

_2nd part in a series on how to write idiomatic Kotlin. Read the_
<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://automationhacks.blog/2019/06/16/vol-1-how-kotlin-eased-my-life-in-a-java-world/" target="_blank"><em>1st
part here</em></a>_._

## Mutable (var) and Immutable types (val) in&nbsp;Kotlin

In Kotlin, variables are typically _**preferred**_ to be declared as `val` and borrows these
constructs from other languages.

Consider below example

We have a `Robot` Class with 3 properties which are `val` by default. We are then creating a new
`Robot` object and printing its properties.

{% gist 3235ac4bb4a7cdbba5ac34b4aa3a1782 %}

Line 6 throws a compiler warning as:  
_Warning:(6, 5) Variable is never modified and can be declared immutable using ‘val’_

Sweet! A language which **explicitly encourages immutability**. 😍 We can update chappie as `val`to
fix this. Read an in-depth explanation of val and var in this
<a href="https://proandroiddev.com/kotlin-for-beginners-immutability-and-the-value-of-val-78ab45b60b57" rel="noreferrer noopener" target="_blank">ProAndroidDev
article</a>

The above code looks a bit repetitive and can be improved:

Observe Line 8–12: We are essentially extracting the properties of `chappie` the robot _every time_
and then printing them. This could be replaced by using a `with` clause to import things into scope.

{% gist 19ff58b4b64d86884d83256253aed757 %}

## Maps

So, what is the most common data structure we all use as programmers. List or Map right?

The simplest way of creating a map, similar to Java is shown below. Here we are using a Hashmap to
create a key value mapping of strings. Pretty standard stuff.

<pre class="wp-block-syntaxhighlighter-code brush: java; notranslate">// Old Java way
    val map = HashMap&lt;String, String&gt;()
    map.put("Stack", "Jeff")
    map.put("Overflow", "Joel")</pre>

However, In Kotlin we can do this in a slightly more readable way. Folks coming from python would
recognize the use of indices to assign a key value in an existing map like below:

<pre class="wp-block-syntaxhighlighter-code brush: java; notranslate">// We can replace .put with indices to make it a little more nicer
    map["Another"] = "Jared"
    map["Hello"] = "World"</pre>

We can also represent map as a builder with just pairs of key values as below

<pre class="wp-block-syntaxhighlighter-code brush: java; notranslate">// Or even create a map with use of builders such as below
    val anotherMap = mapOf(
            Pair("Stack", "Jeff"),
            Pair("Overflow", "Joel")
    )</pre>

However, Even this is not enough. Kotlin gives a much more readable way of representing the above
construct by the use of a `to` infix function. This mostly reads exactly how you would think about
this in your mind.

<pre class="wp-block-syntaxhighlighter-code brush: java; notranslate">val finalMap = mapOf(
            "Stack" to "Jeff",
            "Overflow" to "Joel")</pre>

So now you know of a very clean and concise way of creating a map. However most often than not, you
might want to iterate over this map to achieve some functionality.

Here is the traditional way of doing this:

<pre class="wp-block-syntaxhighlighter-code brush: java; notranslate">// Iterate over map the old way
    for (entry in map.entries) {
        println("${entry.key} -&gt; ${entry.value}")
    }</pre>

While this works, There is a slightly better and concise way of representing the above common logic,
We can directly unpack the result of `.entries` into a Pair and then use it. Much more simpler!

<pre class="wp-block-syntaxhighlighter-code brush: java; notranslate">// Unpacking the result values and using it directly
    for ((key, value) in map.entries) {
        println("$key -&gt; $value")
    }</pre>

## Lifting assignments out of if elses or when blocks

How many times we have written simple code like below: Based on a given status code in an API
response, We decide and do something with the result. Either pass/fail an assertion or in this case
just report the result out.

{% gist 428f673b96460982d0f20da6dcf2605d %}

The above code can be idiomatically written in kotlin by lifting the assignment out of if and the
last statement in conditional (if or else) is automagically returned without need to mention a
return statement and observe that the type of `anotherResult` is also _**type inferred.**_

{% gist 5c3f28d09cd2cfc229863f39534d3c66 %}

Just like if else, we have the powerful `when` clause as a highly powered switch case statement.

Let's assume you have a simple function which depending on different status codes returns what those
status code's mean actually.

{% gist b39d689e147df2392751b2b57cef2469 %}

Now while this code works, It's quite noisy on the eyes and by now you might have got an idea that
there is a much better way of representing this idea in kotlin. We can lift the return out of when
in order to avoid typing this all the time for every case and also group related conditions together
like below:

<pre class="wp-block-syntaxhighlighter-code brush: java; notranslate">fun apiResponsesIdiomatic(response : Response) : String {
    return when(response.statusCode) {
        in setOf(200, 201, 204) -&gt; "Success"
        300 -&gt; "Redirection"
        400 -&gt; "Bad request"
        401 -&gt; "Unauthorized"
        500 -&gt; "Server error"
        else -&gt; "Unknown"
    }
}</pre>

Also, we could even assign this expression to the function just like we did earlier with the **if
else statements**:

{% gist f27e00ddac717314cdbc3de8b51604da %}

## Nullability

Kotlin aims to eliminate Null pointer exception which is also referred to as the
[Billion dollar mistake](http://en.wikipedia.org/wiki/Tony_Hoare#Apologies_and_retractions), by
introducing a set of explicit constructs to mark some type as either Nullable. Also **_by default
all types in Kotlin are non nullable._**

{% gist b6b55de8ffae6f8f6847889e17e53e58 %}

Consider above code:

Do you notice a `?` after String in the argument of `readMeByChar` function (Line 5), This implies
that `text` can be nullable and any attempt to perform an action like getting length of the string
would result in a compiler warning. Since text can be null, we need to explicitly handle for the
null case and that is where kotlin really shines.

<blockquote class="wp-block-quote">
  <p>
    Kotlin forces you to consider nullability as a first class problem and always write code considering it.
  </p>
</blockquote>

In above code `text` has been marked nullable. What if we want to take some action based on if text
has a value or is passed as null? In Kotlin, we have a special operator called **Elvis operator**
`?:`

We can write a statement like below which translates to:

If text is not null then return its value, However if it is not then just assign a default value to
the constant s. This is a concise way of representing this logic and saves us the trouble of writing
an if else statement.

<pre class="wp-block-syntaxhighlighter-code brush: plain; notranslate">val s = text ?: " "</pre>

This is a big topic and can lead to a bit of initial discomfort while understanding. Please read the
[official docs](https://kotlinlang.org/docs/reference/null-safety.html) to grasp this even further

## Functional style

Kotlin is a multi paradigm language and supports a really nice functional style of writing code.

Let's see an example of this below:

We have a simple function which takes nos from 1 to 100 and then if the no is divisible by 16 then
prints hex value of the same.

{% gist 76f8fb248eeab28512ccf3af87023057 %}

Essentially the for with the if condition appears like a **filter map right**? And so we can easily
rewrite this as below with filter and map accepting a lambda function.

<pre class="wp-block-syntaxhighlighter-code brush: plain; notranslate">val list = nums
            .filter { it -&gt; it % 16 == 0 }
            .map { it -&gt; "0x" + it.toString(16) }</pre>

Also `it ->` is optional here and we can remove it to get a bit more conciseness

<pre class="wp-block-syntaxhighlighter-code brush: plain; notranslate">val list = nums
            .filter { it % 16 == 0 }
            .map { "0x" + it.toString(16) }</pre>

Comparing this with the earlier construct with for and if else blocks, this is much more expressive
and clearly communicates the intent.

## Simple considerations

### Raw Strings

In Kotlin, we can enclose long strings with a `Triple quotes """` and have it treated as a raw
string just like python and allows us to easily write a sane string instead of having an army of
`+ and "\n"` to represent even the most basic of JSON structures.

<pre class="wp-block-syntaxhighlighter-code brush: plain; notranslate">// Awesome
    val rawString = """
       Tell me and I forget.
       Teach me and I remember.
       Involve me and I learn
    """.trimIndent()</pre>

<pre class="wp-block-syntaxhighlighter-code brush: plain; notranslate">// Nightmare in Java to even write a simple JSON in a .java file
String hello = "{\n" +
                "  \"Foo\": {\n" +
                "    \"Bar\": \"Woah\"\n" +
                "  }\n" +
                "}"</pre>

### Imports

When working in any professional setup, It can so happen that there are multiple classes with the
same name that you might want to use in the same class. In Java 8 we have to resort to referring to
a fully qualified path for one of the classes.

Well no more. In Kotlin you can simply alias the class with an `as` keyword. This makes the
consuming code so much more readable.

<pre class="wp-block-syntaxhighlighter-code brush: plain; notranslate">import foo.Bar // Bar is accessible
import bar.Bar as bBar // bBar stands for 'bar.Bar'</pre>

<hr class="wp-block-separator" />

Does this list end here?

Well no, Kotlin has lot of goodness hidden which is left to be explored and this series is probably
just the tip of the iceberg.

If you are still a skeptic after reading this. I would just encourage you to take a leap of faith
and try it out. It's so much fun! I promise.

I have so far not encountered even a single Dev who is criticizing Kotlin's feature and for most of
us it brings a breath of fresh air as a multi paradigm language in the JVM universe with modern
languages.

And this wraps up the two part series. If you found this useful. Why not share it with a friend or
colleague. Until next time. Happy coding. Cheers!
