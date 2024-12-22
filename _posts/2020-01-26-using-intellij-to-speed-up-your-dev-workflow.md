---
title: Using IntelliJ to speed up your dev workflow
permalink: /2020/01/26/using-intellij-to-speed-up-your-dev-workflow/
categories:
  - "Coding"
  - "Productivity"
tags:
  - "hacks"
---

_Give your development experience superpowers!_

I do the bulk of my test automation development in Kotlin/Java or Python languages. After the
programming language, a very important component for the dev workflow is a good IDE.

While the purists generally rave about the use of Editors like Sublime, VSCode or even use of
Vim/Emacs over full-fledged IDE's like Jetbrains IntelliJ, Pycharm or Eclipse. The truth is most
modern devs in this day and age use/prefer IDE's for the host of convenience features and speed and
flexibility they provide.

Personally, I am a big fan of IDE's provided by [Jetbrains](https://www.jetbrains.com/), they are
Uber cool and they are generally my tools of choice and quite easily save me a ton of time while
performing refactoring and greatly decrease the development time. Don't believe it?

If you already use it, then Open up `IntelliJ > Help > Productivity Guide` and see how much time it
really has saved me as of writing this in the past 2 years alone. 🙂

![Productivity guide](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-24-at-10.41.51-pm.png)

However,

- Do we really extract the maximum juice out of these tools?
- How many of the IDE's features do we really use on a day to day basis?

Well, fret not. This post will share some of the awesome tips that you can also follow to become
more productive with your editors. I got to know some of these features when the prolific Dev
evangelist <a href="https://hadihariri.com/" target="_blank" rel="noopener">Hadi Hariri</a> from
Jetbrains visited [Gojek](https://www.gojek.io/) Bengaluru and shared these over a meetup talk.

To demonstrate these features, I would be using appium
[Java client](https://github.com/appium/java-client) project but the same features can be applied in
any **Java/Kotlin (IntelliJ IDEA)** project of your choice or **Python project (In Pycharm)**

## IdeaVim

To start with, did you know all Jetbrains editors come with a very good VIM support via IdeaVim
plugin? Vim commands are amazing.

Once you get used to them, your editing and code navigation speed is easily multiplied 2X and it's
so easy to use it within IntelliJ. If you want to know VIM basics, I did write a
[post](https://automationhacks.blog/2018/09/23/vim-the-editor-you-need-but-not-the-one-you-deserve/)
on it some time back.

To install this plugin, either opt for it when freshly installing IntelliJ or
`Go to preferences > Plugins and search for IdeaVim in marketplace`, don't worry, you can always
temporarily disable it and practice first before starting to use it in your day to day workflow.

![Idea vim in plugins](/assets/images/wp-content/uploads/2019/10/image-2.png)

## Search and Go to files

The most common commands that you should be aware of are ironically mentioned right when you open
it.

I use the IntelliJ IDEA classic keybindings, however, you should be able to quickly find the short
cuts for these operations in the binding of your choice (`Look into Preferences > Keymap`)

![Keymap](/assets/images/wp-content/uploads/2019/10/image-3.png)

One of the most useful commands to be used is
<span style="text-decoration:underline;"><code>refactor</code></span>. To launch the actions menu
type `Cmd + Shift + A` and then type the action that you want to use. In this case, refactor to
launch a bunch of context-specific refactoring.

![search for actions](/assets/images/wp-content/uploads/2019/10/image-4.png)

## Search Shortcuts

Double Shift brings up the search console and this is the single place to either

- Search Classes or Files **(Shift + Cmd + N)** with certain names in your project or
- Perform any action **(Shift + Cmd + A)** for example refactoring certain components inside a
  class.

You can also easily learn the keyboard shortcuts for the common operations within the editor by
seeing the shortcut right beside the command on this screen and trust me the investment in learning
these have huge payoffs.

> The no of times that you avoid using the trackpad or mouse is **one time less** that you have to
> context switch while coding and that does make a lot of difference.

### Search by file initials

While trying to find a file, often we just know the name vaguely by memory. In Search, It is
sufficient to just mention the Initials of the file and IntelliJ would list out all the files which
match that criteria

Let's say, for example, I want to search for all test files which start with `A` and have Test
suffix, I can just enter `ATes` and see all the file names which match this.

![Search by file initials](/assets/images/wp-content/uploads/2019/10/image-6.png)

### Search method inside a file matching a pattern

What if I want to search for all methods having`find` keyword inside test files named `AndTes`?

Well you just use a `dot .` in these search queries and you can easily search for even methods
inside classes based on partial pattern search.

In this case, `AndTest.find` would show all the methods with `find` keyword in them. Neat huh?

![Search by file matching a pattern](/assets/images/wp-content/uploads/2019/10/image-8.png)

### Search for file names inside a particular folder

In below example, I am searching for file names starting with `KeyE` under `nativekey` folder by
separating them with a forward slash `/`

`nativekey/KeyE`

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-24-at-10.54.14-pm.png)

### Navigating options all within the search

If you type a forward slash in `/`  you can see different IDE actions that you can take right from
the search bar

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-24-at-10.59.31-pm.png)

## Find usages

You can quickly find out usages of a given function, class, interface, etc by hitting `Cmd + B`,
This saves a ton of time than manually searching for code. You can either navigate right inside the
result pop up or open it in dedicated window by selecting `Open in find window`

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-10.52.51-pm.png)

# A glance at the structure

What if I want to see all the classes and methods that are present in `AndroidTest.java` class?

We can open the **Structure** tab **(Cmd + 7)** and glance at all the available methods with options
to even show **anonymous classes/lambdas** inside the class.

Now, this could be very useful when you have a long class and want to see all the methods and then
quickly navigate to them. Too many methods might hint at a potential refactoring candidate.

![](/assets/images/wp-content/uploads/2019/10/image-7.png)

# Navigation features

## Switcher

To switch between open files and open tabs

Use `Ctrl + Tab` and then to move down continue pressing `Ctrl + Tab` and to move up in switcher use
`Ctrl + Shift + Tab`

This is a useful way to quickly navigate among files and menu options again without using mouse or
trackpad

![](/assets/images/wp-content/uploads/2020/01/switcher.png)

## Recent files

You do not need to remember what files were recently opened. To view recent files accessed, execute
`Cmd + E`

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-9.35.41-pm.png)

## Navigation bar

How many times have you switched the project tree using `Cmd + 1` and gone one level up to open a
file? Before observing this, I know I kept on doing this again and again.

However, IntelliJ has a navigation bar on top of the editor which can be used to very quickly
navigate up the project tree.

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-9.36.24-pm.png)

# Live templates

IntelliJ has a bunch of templates already created which can be quickly used to create a base
skeleton code for many common constructs.

It is also aware of what type of file is currently opened and can show available options by opening
`Cmd + J`, once you select the one that you are looking for, expand this code using `Tab` key

To open these templates and maybe even add your own, open `Preferences > Editor > Live Templates`

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-9.44.40-pm.png)

# Inject language reference

IntelliJ allows us to insert the context of a particular language and allows to work with it within
another file. Seems confusing? Let me explain why this is a super neat feature in IntelliJ.

Let's assume you want to store JSON string inside a Java file. Typically Java 8 does not have
support for multi-line string (Added in
[Java 12 though](https://dzone.com/articles/jdk-12-raw-string-literals))

You can start with a simple string variable.  Press `Option + Enter` and select
`Inject language or reference`

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-9.57.48-pm-1.png)

And then select the file type. Let's say JSON

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-9.58.00-pm-1.png)

Now that we have provided the context, You can again press `Option + Enter`  and then select
`Edit JSON fragment` . This opens up a new window where you can create and edit JSON freely and the
corresponding concatenated string is automagically inserted.

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-10.19.57-pm.png)

# Validate regex inside the editor

Regexes are a very powerful concept to use and learn about.

How many times have you had to write small scratch files with below snippet to test whether a given
string matches a regex? Or test on [regex sites](https://regexr.com/)

I have personally done this many times.

```java
class Scratch {
 public static void main(String[] args) {
 String regex = "\\w+ world!";
 String testString = "Hello world!";
 System.out.println(testString.matches(regex));
 }
}
```

IntelliJ makes this even easier. Given a regex, enter `Option + Enter`  and select **Check RegExp**

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-10.48.21-pm.png)

Enter test strings and IntelliJ would automatically test whether the sample string is a match or
not. Neat right?

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-10.48.47-pm.png)

# Drop frames while debugging

While developing it's very important to be good at debugging. IntelliJ allows a very rich set of
inspection features to know the state of variables/classes at a given point in the code.

In this below example, we have a simple `fooBar()` method which is a wrapper over `foo` and `bar`
methods where `foo` has a debug point.

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-10.59.25-pm.png)

What if we want to move a step back from the current frame? It turns out we can select the current
frame and select `Drop frame` and that would move the debug flow back to `foo` method.

It's amazing how much time this saves since we do not need to rewire the debugging session from
scratch.

![](/assets/images/wp-content/uploads/2020/01/screenshot-2020-01-25-at-10.59.34-pm.png)

And that's it for this post.

Hopefully, this would encourage you to also explore the feature-rich IDE's that Jetbrains provide
and give your automation development a literal nitro boost. (NFS reference anyone?)

What other IDE tricks that you are aware of? Let me know in the comments. If you found this useful,
do share it with a friend or colleague and check out other articles in the
[blog](https://automationhacks.blog/)
