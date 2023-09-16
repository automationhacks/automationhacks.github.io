---
title: Python API test automation framework (Part 9) Running tests in parallel
excerpt: "We explore using pytest xdist plugin to run tests in parallel for our framework"
permalink: /2021/02/23/python-api-automation-framework-part9-running-tests-in-parallel
image: /assets/images/2021/02/api_course_header_9.png
categories:
  - "Test automation"
  - Testing
tags:
  - Python
---

![Python and requests and header](/assets/images/2021/02/api_course_header_9.png)

Logos in header image sources:
[Python](https://commons.wikimedia.org/wiki/File:Python-logo-notext.svg),
[Requests](https://en.wikipedia.org/wiki/File:Requests_Python_Logo.png),
[JSON](https://en.wikipedia.org/wiki/JSON),
[HTTP](https://commons.wikimedia.org/wiki/File:HTTP_logo.svg),
[Cerberus](https://docs.python-cerberus.org/en/stable/_static/cerberus.png)
[ReportPortal](https://reportportal.io/)

This is the ninth and final 👋 post in our series on how to build an API framework using python.

You can read previous parts below:

- [Python API test automation framework (Part 1) Introduction, Setup and Installation ]({% link
  _posts/2020-11-23-python-api-automation-framework-part1-python-and-dependencies-setup.md %})
- [Python API test automation framework (Part 2) Making HTTP requests]({% link
  _posts/2020-11-27-python-api-automation-framework-part2-making-http-requests.md %})
- [Python API test automation framework (Part 3) Writing Fluent assertions]({% link
  _posts/2020-12-07-python-api-automation-framework-part3-adding-fluent-assertions.md %})
- [Python API test automation framework (Part 4) Working with XML using LXML]({% link
  _posts/2020-12-17-python-api-automation-framework-part4-working-with-xml-using-lxml.md %})
- [Python API test automation framework (Part 5) Working with JSON and JsonPath]({% link
  _posts/2020-12-25-python-api-automation-framework-part5-working-with-json.md %})
- [Python API test automation framework (Part 6) API response schema validation]({% link
  _posts/2020-12-28-python-api-automation-framework-part6-api-response-schema-validation.md %})
- [Python API test automation framework (Part 7) Refactoring structure](
  {% link _posts/2021-01-08-python-api-automation-framework-part7-refactoring-structure.md%})
- [Python API test automation framework (Part 8) Adding reporting with ReportPortal](
  {% link _posts/2021-02-03-python-api-automation-framework-part8-adding-reporting-with-report-portal.md %})

---

This one is gonna be short and sweet 😉

As the size of your automated test suites grows from 10 to 100 to 1000 automated cases, the only way
to scale your automated tests is to run them in parallel.

Often Test automation engineers start thinking about parallel runs too late in the game at which
point modifying your automation is a very tedious task. Patterns that work for serial execution
sometimes can be a blocker for parallel runs.

If you are completely new to this problem space and terms like **concurrency, threads, processes and
parallel testing** sound like greek, don’t worry 😉, no one knows about it till they really
encounter it and solve it for themselves. I promise to write a more detailed blog around this topic
in the future. Keep watching this space out for it.

I recommend going through These amazing chapter in
[MIT Open courseware 6.031 course on Software Construction](http://web.mit.edu/6.031/www/fa17/) on:

- [Concurrency](http://web.mit.edu/6.031/www/fa17/classes/19-concurrency/) and
- [Thread safety](http://web.mit.edu/6.031/www/fa17/classes/20-thread-safety/)
- Or read
  [this](https://automationpanda.com/2018/01/21/to-infinity-and-beyond-a-guide-to-parallel-testing/)
  useful post by Andy knight

Done reading? 😇

Let’s proceed.

How can we set up our current framework to run our tests in parallel?

Pytest provides a wonderful plugin called [pytest-xdist](https://github.com/pytest-dev/pytest-xdist)
just for this purpose that makes it quite easy to achieve this

## Setup

Install below modules via pipenv

```zsh
# Install pytest-xdist plugin
pipenv install pytest-xdist
pipenv install pytest-xdist"[psutil]"

# Alternatively
# After switching to example/09_running_tests_in_parallel branch
pipenv install
```

## Running in parallel 🚀

Run below command to run your cases on multiple cores in your machine.

Here `-n` mentions the number of CPU’s to send the tests to. You can either give a fixed no like 2,
3 or `auto` in case you want pytest to determine the no of processes (as per no of CPU cores)

```zsh
python -m pytest -n auto
```

Notice `gw0 [8] / gw1 [8] / gw2 [8] / gw3 [8] / gw4 [8] / gw5 [8]` in run logs, these indicate
different worker processes that pytest-xdist uses to run your tests.

```zsh
platform darwin -- Python 3.8.7, pytest-6.2.2, py-1.10.0, pluggy-0.13.1
rootdir: /Users/gauravsingh/self/course-api-framework-python, configfile: pytest.ini
plugins: reportportal-5.0.8, xdist-2.2.1, forked-1.3.0
gw0 [8] / gw1 [8] / gw2 [8] / gw3 [8] / gw4 [8] / gw5 [8]
......F.
1 failed, 7 passed in 1.63s
```

For a small test suite like this, the cost of multiprocessing results in longer runtime however this
is easily amortized for a large enough test suite.

## Customization

You can tell pytest to run all cases within a single module or all methods in a Test class within a
single process by adding flag `--dist loadscope`

```zsh
python -m pytest -n auto ./tests --reportportal --dist loadscope
```

Pytest xdist plugin provides many useful features like:

- running these tests within a boxed subprocess,
- over different platforms,
- getting unique id for the test run and many more.

If you want to learn more, feel free to checkout their github readme as a starting point.

[pytest-dev/pytest-xdist: pytest plugin for distributed testing and loop-on-failures testing modes.](https://github.com/pytest-dev/pytest-xdist)

## Conclusion

This was the final chapter in this long series, I hope you had as much fun 😏 as I had while putting
this up.

Honestly, this helped me revisit a lot of concepts and clarified my understanding of things. Do not
forget to checkout the full course on
[Test automation university](https://testautomationu.applitools.com/instructors/gaurav_singh.html)
(when it comes out).

I have discussed all these concepts with more depth in the videos.

If you found this post useful, Do share it with a friend or colleague and if you have thoughts, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing and coding.
😄
