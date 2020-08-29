---
id: 819
title: 'Musings on Equivalence partitioning and  boundary value analysis'
date: 2020-06-24T02:36:05+00:00
author: Gaurav
excerpt: What are boundary value analysis and equivalence partitioning testing techniques? In this post we would understand these with an example.
layout: post
guid: http://automationhacks.blog/?p=819
permalink: /2020/06/24/equivalence-partitioning-and-boundary-value-analysis/
jabber_published:
  - "1592966167"
publicize_twitter_user:
  - automationhacks
advanced_seo_description:
  - ""
amp_status:
  - ""
spay_email:
  - ""
email_notification:
  - "1592966171"
publicize_linkedin_url:
  - null
timeline_notification:
  - "1592966171"
image: /wp-content/uploads/2020/06/efe-kurnaz-rncpixixooy-unsplash.jpg
categories:
  - Testing theory
---
<figure class="wp-block-image size-large is-resized is-style-rounded"><img loading="lazy" src="https://i1.wp.com/automationhacks.blog/wp-content/uploads/2020/06/efe-kurnaz-rncpixixooy-unsplash.jpg?resize=342%2C513&#038;ssl=1" alt="" class="wp-image-826" width="342" height="513" data-recalc-dims="1" /><figcaption>Photo by [Efe Kurnaz](https://unsplash.com/@efekurnaz?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://automationhacks.blog/s/photos/wall?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)</figcaption></figure> 

Testing is a complex and nuanced field with different aspects to it based on the domain and specific context that you are testing in. However, there are some **first principles** which are timeless and can be applied in many different use cases

Every budding tester should be aware of these. This is a first post in a series of such principles.

Boundary value analysis and equivalence partitioning are test design techniques and often go hand in hand. They are applicable in a wide variety of different situations, most commonly used when you have to design test cases for an app or component that can have a large set of possible inputs.

Let's break it down and understand what they mean.

## An example

Ah, I knew you wanted to skip the theory and jump right in. 😉

Think about this situation:

What if you had to design test cases for a Text box which is used to enter a phone no.

Let's say you have following business rules to validate:

  * Phone nos must be between 10 to 13 digits
  * Phone nos must have positive integers (0 &#8211; 9)

How would you think about designing test cases for this field?

<blockquote class="wp-block-quote">
  <p>
    It's often useful to think about <strong>&#8220;What if</strong> <strong>I do X or Y or Z</strong>, <strong>How should my app respond</strong>&#8221; and understand more about how the app work/should work and form a <strong>model</strong> in your mind that helps you explore and then later design cases.
  </p>
</blockquote>

Here are some cases that we can think about:

  * We can test for all possible phone nos having length of 10 to 13 digits. However, That would be a very huge no of cases and possibly inefficient and expensive to do.
  * Should we take one 10 digit no, one 11 digit, one 12 digit no until 13? Ah, Good idea. Well you can do that, but ask yourself are you getting any unique information about the field by testing all these cases?
  * What if we try phone nos with exactly 10 digit and 13 digit? That would certainly be useful. What if the developer missed adding an **equal to (=)** in the `if` condition for this fields error validation? 😇 Rare, but possible.
  * What happens if we try a phone no less than 10 digit? Or more than 13 digits? Well, that should be invalid as per our said business rules. 
  * Can I enter negative nos? In some countries we have **spaces and hyphens** as valid delimiters for phone no.
  * Can I enter a string here? Again a violation of the business rules. 
  * What if I don't enter anything? 

Good, with those questions we have a good idea of some paths we can take to test this field. 

Did you notice, even while coming up with test cases for this text box, you have subconsciously considered some boundary conditions and set of equivalence classes.

## Boundary values

Boundary value quite simply implies identify the boundary conditions for whatever app, component, logic you are testing and test around it. 

In this hypothetical case: 

Given the rule that a valid phone no must be between 10 &#8211; 13 digits, Its worthwhile to test with a phone no having 9 digits, 10 digits, 13 digits and maybe 14 digits (If allowed)

## Equivalence partitioning

What about equivalence partitioning? The term is a quite a fancy way of saying: 

If a set of inputs are logically similar then testing for just one of them is as good as testing with each and every possible combination.

In the above case: 

It would be fine to test with either one of 11 or 12 digit no. Since both of them fall within the logical classes of phone nos between 10 &#8211; 13.

## Conclusion

Taking these principles a bit further in your work, You can challenge yourself to think about what are the app boundaries you are testing and ensure that you test around it

Also think about how you can break the app into equivalence classes to ensure you take a good representative value out of an entire set of possible values which potentially gives you the same coverage instead of trying to run for every possible value under the sun.

If you found this post useful to you. Feel free to share it with a friend or colleague. Until next time. Happy testing! 👨🏻‍💻

## References:

If you want to read a bit more about these, below are some good resources.

  * [Guru99 post on BVA and equivalence partitioning](https://www.guru99.com/equivalence-partitioning-boundary-value-analysis.html)

  * [Boundary value analysis by Evil tester](https://www.youtube.com/watch?v=H6IRY98Gu44)