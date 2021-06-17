---
title: Plain text note taking system using markdown for technical notes
guid: http://automationhacks.blog/?p=322
permalink: /2019/10/19/plain-text-note-taking-system-using-markdown-for-technical-notes/
categories:
  - Productivity
---

Hello there,

As an engineer working in tech, one of the most important habits to develop over time is your
knowledge base. With each passing month, your skills would improve and you would constantly learn
new technologies or frameworks.

It's important to commit the important ones to some permanent store which is easily searchable, and
can act as a easy point of reference for you in the future.

## Existing note taking apps

I have personally used and tried different note taking apps like
[Microsoft OneNote](https://www.onenote.com/?404&public=1), [Evernote](https://evernote.com/) and
quite recently [Notion](https://www.notion.so/) for this purpose and while each one of them provides
a set of features for note taking and organization into categories for instance Notebook,
Subsections in OneNote or notes with tags in Evernote and notion which has the ability to create
quite rich pages with different sort of connections.

### Disadvantages of using proprietary note taking tools

With all the benefits and convenience that these tools bring, there are obvious disadvantages like:

1. **Dependence** on the app developer to implement essential features e.g. OneNote does not have
   code blocks
2. Some of these tools require you to pay **substantial subscription fees** on a yearly/monthly
   basis in exchange for using advanced features. For instance: Notion has the limit of just 1000
   blocks in the free plan and evernote has limit on how much data you can upload while under the
   free plan.
3. Since your data is stored in their servers, you are subject to **network latency and occasional
   sync issues** and features like search is something that they provide and control.
4. Your data is **locked in their proprietary format** and sharing it with other folks is not as
   straightforward. Every person might have different preferences of note taking tool (Using MS
   word, Google docs, evernote etc) and hence its difficult to collaborate on these documents.
5. Your **data is not future proof**. What if one of these companies decide to kill these products?
   In that scenario, All the time and energy spend in organizing your notes would have to be
   reinvested into the new platform.
6. **Clunky UI and occasional bugs** in their apps make for a less than ideal experience and in most
   occasions these tools are rarely truly cross platform. (Linux, Mac, Windows, Android)

## The solution: Plain text note taking

So is all hope lost? Are we stuck at the mercy of these note taking apps?

Some time back, I discovered plain text note taking using
[markdown](https://guides.github.com/features/mastering-markdown/) as a alternative and since
switching to it, have not looked back on any of these apps again.

### Advantages of plain text note taking

There are many advantages of using markdown for your note taking requirements.

1. Your **data is future proof**: Plain text has been around since decades and would probably
   continue to be so regardless of how many tools arrive.
2. It is **machine readable and is truly cross platform**. Notes written are accurately formatted
   and represented in the same way across all your different platforms
3. **Writing in plain text takes away all the distractions** and let's you focus on the core
   activity of writing, no unnecessary time is wasted on trivial formatting gimmicks and templates.
4. The note **can be easily published on the web as HTML or to a PDF** if it needs to be shared with
   others.
5. Using a cloud storage provider like Dropbox or Google Drive, you can easily sync your notes
   across different devices and that's pretty much all you need. There is no need to spend on extra
   subscriptions etc. You own your data.

## The workflow

So how does my workflow look like after switching to plain text note taking?

![](/assets/images/wp-content/uploads/2019/10/image.png)

Snapshot of my notes structure. Opened in VSCode with markdown preview on the side.

It's quite simple really.

### Markdown files in organized folder structures inside a Git repo

- I have a private GitHub repo which is synced to my notes dir where I have the notes arranged as
  different folders and subfolders of relevant categories. **Why git?** Well, it helps me have a
  reference of when certain changes were made in the form of well defined commit messages and I
  always have the ability to go back to a change in case that's needed.

### Edit files in VS Code (PC)/iaWriter (android). Synced with Dropbox

- [VSCode](https://code.visualstudio.com/) is a amazing cross platform editor from microsoft and has
  a good level of inbuilt markdown support and also a preview option to see how your changes look
  like. It has a **markdown lint inbuilt** that ensures you write correct markdown syntax.
- Markdown code formatted blocks are amazing to store code snippets in.
- Additionally these notes are synced with Dropbox and the remote GitHub repo, this means, I always
  have a way of getting at my notes via either web in case i don't have a personal laptop handy
- In case, I need to make edits to certain files on a mobile device, all that's needed is an app
  which has the option to sync with the cloud storage of your choice. I have recently started using
  iaWriter and it works quite well for my needs.

### First class search experience

- Searching for some file is as simple as opening the folder in VS code and doing a file search
  based on some keyword or use `find` or equivalent command on the terminal. It's blazing fast with
  zero latency.
- If needed, I can always make use of GitHub or cloud storage's search capabilities as well.

In conclusion, If you are facing similar issues with your current note taking apps, You might want
to consider taking the plunge into the world of plain text note taking.

I'm sure you will not regret it. The freedom, speed and flexibility is amazing and more than makes
up for the lack of fancy features. It's a bit of work initially but has amazing payoffs.

Are you convinced?

So, what are you thoughts on the subject? Happy to know them in the comments. In case you find this
useful, please feel free to share it with a friend or colleague. Until next time. Cheers!
