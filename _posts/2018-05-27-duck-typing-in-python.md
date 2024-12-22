---
title: Duck Typing in python
excerpt: "Understand what duck typing in python means with an example"
permalink: /2018/05/27/duck-typing-in-python/
categories:
  - "Coding"
tags:
  - "Python"
---

> Quite simply put, Duck typing gives a programmer the ability to not worry about the type of a
> class rather perform the required operations.

Let's take a simple code example as below:

{% gist f82126b921e80519c9fb19d95f6556e7 %}

If we execute this code:

```text
Quacked
Louder Quack
Traceback (most recent call last):
  File "/Users/gaurav/personal/development/grasp-python/base/advanced/duck_typing.py", line 33, in <module>
    MakeItQuack(Eagle())
  File "/Users/gaurav/personal/development/grasp-python/base/advanced/duck_typing.py", line 29, in __init__
    bird.quack()
AttributeError: 'Eagle' object has no attribute 'quack'
```

Observe here we are passing an object `bird` to `MakeItQuack` class constructor and invoking
`quack()` on the passed object.

Thus classes which have an implementation of `quack` method will be able to call _(Duck, AnotherDuck
objects)_ whereas we get a `AttributeError` if we try to pass an object which does not provide an
implementation of `quack()`&nbsp;,herethe `Eagle` class.

This is the essence of duck typing. Having the ability to do this without writing an Interface is
really awesome.

In case you want to know more, you can further read
[voidspace](http://www.voidspace.org.uk/python/articles/duck_typing.shtml[/embed) blog on the same
topic
