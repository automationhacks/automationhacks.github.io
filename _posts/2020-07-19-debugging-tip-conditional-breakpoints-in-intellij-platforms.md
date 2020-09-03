---
id: 942
title: "Debugging tip: Conditional breakpoints in IntelliJ platforms"
date: 2020-07-19T01:59:11+00:00
author: Gaurav
excerpt:
  "Useful debugging feature in IntelliJ based IDEs: Put a breakpoint which stops only when a certain
  condition matches."
layout: post
permalink: /2020/07/19/debugging-tip-conditional-breakpoints-in-intellij-platforms/
jabber_published:
  - "1595123953"
timeline_notification:
  - "1595123955"
email_notification:
  - "1595123955"
image: /assets/images/wp-content/uploads/2020/07/conditional_breakpoint.png
categories:
  - Kotlin
  - Programming
  - Tools and tricks
---

![Conditional breakpoints](/assets/images/wp-content/uploads/2020/07/conditional_breakpoint.png)

Hi there, I recently became aware of an amazing debugging feature in
**[Jetbrains IDE's](https://www.jetbrains.com/)** that has made my debugging workflows so much
easier and fast. They are called as **Conditional breakpoints**

## Why not a simple breakpoint

Often while developing tests you might want the debugger to **pause** only when a specific condition
happens.

We know we can always put a breakpoint on any **line or function call** and run our test in debug
mode and then use debugger to step into/step over etc till we reach the point where we want to debug
from.

However many times, this can become tedious quite quickly if you have many rows of data in your data
driven test as you need to **press continue** till you reach the row/record which are you interested
in.

Conditional breakpoints provide a quick way to workaround this problem.

Let's see how

## Conditional breakpoints to the rescue

To show this in action, I will assume a test program which given a number `num` determines if it is
a prime or not and a simple test for this.

{% gist d366955370d58dc2ca40c185b62cd829 %}

Let's assume we want to debug something when the value of `i` becomes `3` (this could be
replaced with any condition that you care about in your program)

You can click on the line no (in this case `12` in below screenshot) to add a breakpoint as you
normally do. But if you **right click** on the breakpoint then you can see the option to add a
condition. Any condition that you add here would get evaluated every time the program flow comes to
this line and if the condition evaluates to a **true** and only then would the breakpoint would get
triggered.

![Conditional breakpoint](/assets/images/wp-content/uploads/2020/07/conditional_breakpoint.png)

As you can see below, the program breaks when the condition matches.

![on breakpoint](/assets/images/wp-content/uploads/2020/07/on_breakpoint.png)

## Conclusion

This is very useful and is available in all the IDE's provided by Jetbrains. With this
debugging feature, I can easily make the debugger stop at the condition that I can about, without
changing the code/test data that's feeding into the method. Go ahead try it, You will wonder
how you even debugged earlier without this feature.

If you found this post useful, Do share with a friend or colleague. Until next time. Happy
debugging. 😇

## Further read

- [Conditional breakpoints in Pycharm](https://www.jetbrains.com/pycharm/guide/tips/conditional-breakpoints/)
- [Using IntelliJ to speed up your dev workflow](https://automationhacks.blog/2020/01/26/using-intellij-to-speed-up-your-dev-workflow/)
