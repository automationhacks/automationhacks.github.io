---
title: How to do reverse lookup enum constant by value in Kotlin
layout: post
permalink: /2019/12/11/how-to-do-reverse-lookup-enum-constant-by-value-in-kotlin/
categories:
  - "Coding"
---

This is a neat trick I discovered recently

[enums](https://kotlinlang.org/docs/reference/enum-classes.html) are a very useful concept in
programming and allow us to define constant values which can easily hold grouped data and even
declare members

I use them heavily in my automation code to define constant values and they work very well when we
have the define different branches in `when` clause in kotlin to maybe perform different sort of
actions

## A common use case

One common use case for me is when I want to do **enum constant lookup using its value**. For
example, I might declare different configurations for my tests and based on these values, I might
want to take different actions, trigger some flows or perform some assertions

Let's understand this with an example

{% gist 7d7c10f16e207006786dc43cd5d4f3c0 %}

In the above example, we have defined an enum class called `Mouses`which has all different mouses
and a short brand name for each.

If we want to get the **enum constant** value which has the **value = &#8220;logi&#8221; **then we
can write a simple `foreach` loop in kotlin to iterate over all the values and if the desired value
is found (Ln 17 &#8211; 21) then assign it to the temporary enum variable (Ln 15)

Fair and simple enough right.

However, we would have to write this simple logic again and again for all the different enum
constants that we declare.

## A slightly better way using companion objects

The above code gets the job done, however, this could be written in a slightly more elegant way.

Below is the updated code

{% gist 60259d002899666c563bd066de609c48 %}

Let's understand this:

Ln 10 &#8211; 13, we have declared a
`<a href="https://kotlinlang.org/docs/tutorials/kotlin-for-py/objects-and-companion-objects.html">companion object</a>`
block to tie a member and a function to the enum class itself rather than its instance

Ln 11: We have a private immutable variable called `mapping` which has the mapping of all the enum
constants with their values. This is done by using `associateBy()` which is called upon the
`values()` array

if we peek into the code for this function, we can see that it returns a `Map<K, T>`, where K is the
value of the enum constant and T is the actual constant itself

![](/assets/images/wp-content/uploads/2019/12/screenshot-2019-12-11-at-10.33.57-pm.png)

Finally, we have a `fromValue()` method which accepts the enum constant value and returns the
associated constant from the mapping variable. If for some reason the value does not match an
existing constant, then we raise an exception **like below (Ln 19)** with the name of the class

```text
java.lang.IllegalStateException: Look up failed for class experiments.MousesV1
```

Now we can easily call this `fromValue` method on the enum constant and get the associated constant
(Ln 18)

And that's it. This has already made my code look much more concise and made it easier for me to use
enums. Hopefully, you found this useful.

Until next time. Happy coding.
