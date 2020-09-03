---
id: 45
title: "Vim: The editor you need, but not the one you deserve"
date: 2018-09-23T13:48:49+00:00
author: Gaurav
layout: post
guid: http://automationhacks.blog/2018/09/23/vim-the-editor-you-need-but-not-the-one-you-deserve/
permalink: /2018/09/23/vim-the-editor-you-need-but-not-the-one-you-deserve/
publicize_twitter_user:
  - __gaurav_singh
publicize_linkedin_url:
  - null
categories:
  - Programming
  - Tools and tricks
---

Hi there! So apart from the obvious reference to the Dark knight trilogy, I think this is quote in a
small way highlights how great Vim is. Once put in practice you it really feels like this editor is
one of the hidden gems which most coders are scared of.

I am a relative new convert and started learning and using Vim about couple of months now and let me
tell you **it does all that is promised and more in all the blogs** you might have read.

---

### What is vim and why should you&nbsp;care?

If you have never heard of vim, you can check out
<a href="https://www.vim.org/" target="_blank">vim.org</a> but essentially it is a text editor like
many others.

Where vim makes a difference is that it has different modes which allows you to move around your
code/text and change it much faster and really increases productivity.

Also vim is pretty much ubiquitous, you can find it pre installed in most of the linux flavours and
can also be installed pretty easily on
<a href="https://www.vim.org/download.php" target="_blank">Windows</a>. If you are working with
files on ubuntu servers/containers, you can bet you would find vim in there.

The big benefit for me as a programmer is the
<a href="https://vim.rtorr.com/" target="_blank">keyboard bindings</a>. Once you learn vim commands,
you do not have to learn editor specific keyboard bindings and remember them when you switch around,
you can always use the same muscle memory and become awesome at editing be it code any text.

Sounds good? Lets dig in a little bit and see how it works

---

### Vim modes

There are 3 main modes in vim:

1. **Normal mode**: Move around the text and execute commands. Vim by default starts in this mode
   and you get back to it from other modes by pressing `ESC`
2. **Insert mode**: Insert/delete text. This Works similar to other text editors. To get in press
   `i`
3. **Visual mode**: Select some text and then execute commands on top. To get into this press `v`,
   vim by default goes in visual mode if you select something using trackpad or mouse.

We would talk about these modes in more details later.

> Tip: After using vim for sometime you would get into the habit of pressing `ESC` after every
> change that you make.

---

### Basic commands

As with learning any thing new you always need to know the basics. Vim has so many
<a href="https://www.vim.org/docs.php" target="_blank">resources</a> out there to learn and become
better. However in this article i would make a humble attempt to walk you through some of the basic
commands which i most commonly use.

Create any new file or open one using `vim <file_name>` on the terminal.

### Moving around

As programmers most of the time we spend is actually navigating in a source file and understanding
how the code works right? In vim, remember you do not need to use mouse or even arrows keys. We
would usually use the 26 alphabet keys and some others to do most of the job.

```text
In normal mode:

h: Move left
l: Move right
j: Move down
k: Move up
```

Every key stroke moves the cursor one character at a time.

> Tip: Vim has this super cool feature called **modifiers** wherein you can **repeat the same
> command multiple times by prepending a number in-front of it**. Example if you want to move 10
> lines in upward direction just press `10k` or 20 chars to right then `20l` and so on…

As you start, practice using these commands and after a few weeks these would become muscle memory
for you.

### Moving even faster&nbsp;😉

You might be thinking thats good but do i need to always press 20 followed by some `hjkl` command to
move to some place where i want to edit? How would i even know how many chars to end of the word
where i currently am?

Not to worry, Vim has some more commands to make this easier

```text
w - Skip to start of next word
W - Skip to next word (excluding symbols)
e - Move to end of word
E - Move to end of word (excluding symbols)
b - Move to beggining of a word in backward direction
B - Move to beggining of a word in backward dir direction (excluding symbols)

Symbols: Special characters like brackets/commas etc.
```

Using these you can quickly move around words and remember you can always prepend a modifier to move
even faster;

Lets take an example:

Below is a very simple code for a function in python to print name and age.

```python
def foo(name, age):
    print("My name is" + name)
    print("My age is" + age)
```

Move cursor to def and then try pressing `w` a few times and then repeat same thing with `W`&nbsp;,
did you see any difference? `w` would go to start of each word, even taking into account the comma
or brackets in between, however `W` would exclude symbols and just be concerned with the actual
words.

Once you master this, moving around code is so much easier.

---

### Lets Insert some&nbsp;texts

So once you are able to move around in a file, the next natural thing to do is to insert some text
right? Go ahead and play around a little with getting into and out of insert mode using `i` and
`ESC` and enter some text

Vim makes it easily for you to get into **insert mode** using different commands.

So as an example lets say you want to start writing in a new line after you current cursor position,
you can either do:

- Press `i` to get into insert
- Press arrow keys to go to end
- Press `ENTER` to go to next line
- Then type the text that you want to enter

Or you can just press `o` and it would insert a new line from currrent cursor position and you can
start typing away.

Below are few other variations of these commands. I would encourage you to try it out. Having these
in mind makes it super easy to start editing you files.

i - insert before current cursor position
I - insert at start of line (similar to Ctrl + Left arrow key)
a - insert after current cursor position
A - insert at end of line
o - opens a new line after current line
O - opens a new line before current line

> Tip: Typically in vim every command has a **Caps** version as well which does similar operation
> but mostly for a line or some other scope.

> Example: If you want to enter a char after current cursor you press `a` however `A` lets you
> insert at end of the line. Sweet right?

### Editing:

So as coders, most of the times we need to either rename a variable or function name rather than
just inserting text right?

Lets see how we can do editing using vim.

#### Copy Paste (Ctrl + C/ Ctrl +&nbsp;V):

Below is vims way of doing copy or paste. However usually if you want to copy something you need to
**select it first**. So to do that `Visual mode` comes really handy. Essentially you just need to go
in visual mode `v` and then select the word/sentence that you want to copy using moving around
commands `hjkl` or `wWbBeE` and then just press `y`

y - yank a.k.a copy
Y - yank current line
p - paste (after the cursor)
P - paste (before the cursor)

#### **Cut (Ctrl +&nbsp;X)**

Thats great, so you can copy and paste now, but if you want to delete some word or line? Use below
commands.

x - delete single character (equivalent to DELETE)
X - deletes single character before current cursor position (equivalent to BACKSPACE)

d - delete based on some more modifiers (some variations below)
dw - delete word
de - delete till end of word
dE - delete excluding symbols 
dW - delete to next word excluding symbolds

D or dd - delete current line

> Tip: delete command is actually like CUT so anything that is deleted can always be pasted using
> `p`

Finally every one makes mistakes, programmers even more so. We go through multiple iterations of
refactoring the code before we are happy so what if you deleted some thing by mistake. Don’t worry,
just press `u` to **UNDO** your last action.

#### Insert or&nbsp;change:

If you want to just edit a single char or sentence, use below.

r - replace single character
R - replace all following characters (Enter insert mode, instead of insert it basically modifies what even is present)

### Saving files/Exiting:

So till now you have been able to move in a file, able to insert or cut/paste texts and so on… How
do you make sure your work is saved? 😉

:w &lt;file_name&gt; - save untitled file to specified name
:w - write the changes to the file
:q - quit, if there are changes since last write we would get an error.
 To override this error and still quit without saving, type :q! (with exclamation)

> Tip: Commands can always be combined so to quit the file with also write changes use&nbsp;`:wq!`

### Vim with other editors/IDE’s:

This might hurt the vim purists out there a little, but i like most coders out there use popular
IDEs for their development workflows like IntelliJ for Java or Pycharm/Vscode for python. So how
does this vim knowledge get applied there?

The good news is most of the editors for Jetbrains offer a vim emulation plugin called `ideavim` and
similarly VS code also provides a `vim extension`

On being activated you get most of the vim command behavior and this way you can use it in your day
to day coding.

### **Summary:**

These command above are by no means exhaustive and there is _always more_ to learn with vim.

Remember if you are able to learn one new thing everyday you would be a expert in no time. Also i
highly recommend to start using these in you daily activities to really make it practical for your
use.

There are still some more concepts to get around with vim which i would cover in a subsequent blog
like registers, buffers, customizing your vim.

Please share this with your friends if you found it useful and let me know if you have comments.
Cheers!
