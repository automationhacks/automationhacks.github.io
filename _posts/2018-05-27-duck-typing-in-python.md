---
id: 43
title: Duck Typing in python
date: 2018-05-27T05:55:17+00:00
author: Gaurav
layout: post
guid: http://automationhacks.blog/2018/05/27/duck-typing-in-python/
permalink: /2018/05/27/duck-typing-in-python/
categories:
  - Programming
  - Python
---
<blockquote class="wp-block-quote">
  <p>
    Quite simply put, Duck typing gives a programmer the ability to not worry about the type of a class rather perform the required operations.
  </p>
</blockquote>

Let's take a simple code example as below:<figure class="wp-block-embed is-type-rich">

<div class="wp-block-embed__wrapper">
  <div class="gist-oembed" data-gist="f82126b921e80519c9fb19d95f6556e7.json" data-ts="8">
  </div>
</div></figure> 

If we execute this code:

<pre class="wp-block-preformatted">Quacked<br />Louder Quack<br />Traceback (most recent call last):<br />  File "/Users/gaurav/personal/development/grasp-python/base/advanced/duck_typing.py", line 33, in &lt;module&gt;<br />    MakeItQuack(Eagle())<br />  File "/Users/gaurav/personal/development/grasp-python/base/advanced/duck_typing.py", line 29, in __init__<br />    bird.quack()<br />AttributeError: 'Eagle' object has no attribute 'quack'</pre>

Observe here we are passing an object `bird` to `MakeItQuack` class constructor and invoking `quack()` on the passed object.

Thus classes which have an implementation of `quack` method will be able to call _(Duck, AnotherDuck objects)_ whereas we get a `AttributeError` if we try to pass an object which does not provide an implementation of `quack()`&nbsp;,herethe `Eagle` class.

This is the essence of duck typing. Having the ability to do this without writing an Interface is really awesome.

In case you want to know more, you can further read [voidspace](http://www.voidspace.org.uk/python/articles/duck_typing.shtml[/embed) blog on the same topic