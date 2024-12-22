---
title: Python API test automation framework (Part 1) Introduction, Setup and Installation
excerpt:
  "Introduction to the course and setting up python and required dependencies for building an API
  framework"
permalink: /2020/11/23/python-api-automation-framework-part1-python-and-dependencies-setup
image: /assets/images/2020/11/api_course_header_1.png
categories:
  - "Software Testing"
  - "Python"
  - "Programming langauges"
  - "Backend automation"
tags:
  - "Python"
  - "API testing"
---

![Python and requests and header](/assets/images/2020/11/api_course_header_1.png)

Logos in header image sources:
[Python](https://commons.wikimedia.org/wiki/File:Python-logo-notext.svg),
[Requests](https://en.wikipedia.org/wiki/File:Requests_Python_Logo.png),
[JSON](https://en.wikipedia.org/wiki/JSON),
[HTTP](https://commons.wikimedia.org/wiki/File:HTTP_logo.svg)

Hi there, 👋

I am currently building 🏗️ a course for
[Test automation university](https://testautomationu.applitools.com/) on **"Building an API test**
**framework with Python"** and had this idea of why not have a blog for each chapter as I go along
to serve as a supplement to the video course content while also being accessible to folks who are
more inclined to read blogs and ensuring I personally stay focused and don't procrastinate on this
😁. You are all there to hold me accountable to do this. 🤝

These posts are gonna come out in order as the course is being developed and much before the actual
course is published. The course is gonna dive deep into most of the aspects mentioned here.
Hopefully these would provide the test automation community valuable insights and guidance on how to
approach building API automation frameworks at their workplace using python

Below is a non exhaustive outline of what I have planned for this course at the moment:

- Chapter 1: Setup up python and virtualenv on mac or windows
- Chapter 2: Making HTTP requests
- Chapter 3: Adding fluent assertions
- Chapter 4: Working with XML
- Chapter 5: Working with JSON
- Chapter 6: API data/schema validation
- Chapter 7: Adding reporting
- Chapter 8: Running tests in parallel

This is also a chance for you to interact and provide ideas about which direction this course could
take. Your perspective would be very valuable. Feel free to provide your comments using comment
section below or DM me on twitter `@automationhacks` in case you would like to get some thing else
added as well within this problem space.

## Introduction to building API automation framework with Python

Writing **Functional API automation** is a great way of getting fast and stable feedback about your
system as well as exercise business flows and logic as compared to UI tests. In this course we would
see the building blocks for a robust API automation framework using python to test your API’s.

We would cover automation development practices that you can follow and use different useful
libraries in the python ecosystem to build our framework.

All the source code would be available on GitHub
[course-api-framework-python](https://github.com/automationhacks/course-api-framework-python)

## Setup and installations

Before we begin building our framework for API testing, let's make sure we have the basic
dependencies already setup

If you are completely new to Python/pytest then I would recommend you check out the courses on
[Test automation university](https://testautomationu.applitools.com/) to familiarize yourself with
the basics since this course assumes you have some experience with python already

- [Python Programming - Jess Ingrassellino](https://testautomationu.applitools.com/python-tutorial/)
- [Introduction to pytest - Andrew Knight](https://testautomationu.applitools.com/pytest-tutorial/)

Let's dive in now 🤿

### Setting up python and dependencies

As a prerequisite to this tutorial, Please ensure you have `python3` installed on your machine. If
not already installed, you can go to [python.org](https://www.python.org/downloads/) and download
the latest version of python for your OS and run the installer

Alternatively if you are on mac/linux and have homebrew/linuxbrew already installed then you can
install python using below command

```zsh
brew install python
```

Let’s test to make sure python is installed and available from the command line

```zsh
python3 --version
```

Finally execute below to ensure you can access python REPL and you are all set

```zsh
python3
Python 3.8.6 (default, Oct 21 2020, 11:06:14)
[Clang 11.0.3 (clang-1103.0.32.62)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

### Setting up virtualenv

With python setup. The next step that we need to take care of is to set up a virtualenv in which we
can install all the required packages. You can just install modules directly on your base python
installation but its an accepted best practice to use virtualenvs

I've already written a blog with details on how to you use `pipenv` to create a virtualenv for your
project, please follow the same and setup pipenv and an empty env

you can refer to it
[here]({% link _posts/2020-07-12-how-to-manage-your-python-virtualenvs-with-pipenv.md %})

With this, we have our virtualenv ready for use.

### Install requests

To install any python module using pipenv you can use below command

```zsh
pipenv install <module_name>
```

Let's install `requests` which we would use to actually make HTTP requests.

```zsh
pipenv install requests
```

We can always check the package is installed by executing below (while inside the virtualenv)

```zsh
pip freeze
```

We will also use pytest as the test framework of choice

```zsh
pipenv install pytest
```

If you use pycharm as the editor of choice then you would need to select the newly created
virtualenv as the project interpreter by following below steps

- Open Preferences/Settings
- Search for Python interpreter
- Click on Gear icon and then click on Add
- Select Existing environment
- Select path to bin/python for the created virtualenv (usually in `WORKON_HOME` dir setup in your
  shell)

![Selecting virtualenv in pycharm](/assets/images/2020/11/select_virtualenv_in_pycharm.png)

Also, let's make sure pycharm knows that we intend to use pytest as the default test framework to
run cases by going to

- Open preferences/settings
- Search runner
- Under `Python integrated tools > Testing` select default test runner as pytest

![Selecting pytest as the test runner in pycharm](/assets/images/2020/11/select_pytest.png)

## Conclusion

And that all we need to get started with building our framework. We will add other modules when we
discuss them in further chapters. Stay tuned for the next post on how to make an HTTP request using
requests module

You can find the complete code for this course on Github at
[automationhacks/course-api-framework-python](https://github.com/automationhacks/course-api-framework-python)

If you found this post useful, Do share it with a friend or colleague and if you have thoughts, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing and Coding.

## References

- [How to manage your python virtualenvs with Pipenv](https://automationhacks.io/2020/07/12/how-to-manage-your-python-virtualenvs-with-pipenv/)
- [Python virtualenvs: A primer](https://realpython.com/python-virtual-environments-a-primer/)
