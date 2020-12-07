---
title: Python API test automation framework (Part 3) Adding fluent assertions using assertpy
excerpt:
  "Using a good assertion library can supercharge your automation framework. In this post we see how
  assertpy library could be useful and see some examples of its capabilities in an API framework"
layout: post
permalink: /2020/12/07/python-api-automation-framework-part3-fluent-assertions-using-assertpy
image: /assets/images/2020/12/api_course_header_3.png
categories:
  - "Test automation"
  - Testing
tags:
  - Python
---

![Python and requests and header](/assets/images/2020/12/api_course_header_3.png)

Logos in header image sources:
[Python](https://commons.wikimedia.org/wiki/File:Python-logo-notext.svg),
[Requests](https://en.wikipedia.org/wiki/File:Requests_Python_Logo.png),
[JSON](https://en.wikipedia.org/wiki/JSON),
[HTTP](https://commons.wikimedia.org/wiki/File:HTTP_logo.svg)

This is second post in a series on how to build an API framework using python.

You can read previous parts below:

- [Python API test automation framework (Part 1) Introduction, Setup and Installation ]({% link
  _posts/2020-11-23-python-api-automation-framework-part1-python-and-dependencies-setup.md %})
- [Python API test automation framework (Part 2) Making HTTP requests]({% link
  _posts/2020-11-27-python-api-automation-framework-part2-making-http-requests.md %})

An integral part of any test automation framework is how you perform assertions ✅ 🔴. You can also
argue that it's the essential bread and butter of test automation. Ever seen a test that does not
assert anything? 🤔

While you can always choose what comes out of the box with your language or test framework, or even
come up with your own wrappers. It’s always a good idea to not **reinvent the wheel** ☸️ and
leverage a good assertion lib to save you some valuable implementation time.

For python, there are many options available. However I particularly like the **assertpy** library
for its fluent assertion capabilities and the fact that it has excellent support for working with
native python data structures like **list, set, dict** among other primitive data types.

It is heavily inspired from [AssertJ](https://assertj.github.io/doc/) library which in itself is
quite popular in the Java community and used in many popular open source tools

## Starting with fluent assertions

How to start with fluent assertions with assertpy, you may ask?

Like any other python module, You should start by adding it to your virtual env by using below

```zsh
pipenv install assertpy
```

Also, reading the exhaustive and well written Github readme is an excellent starting point as it
provides you with a huge list of operations and methods that are possible with assertpy. You can
learn more on [assertpy/assertpy](https://github.com/assertpy/assertpy)

## Basic assertions

Let’s see some basic assertions for our use cases and I would leave the rest to you to explore as
and when you encounter certain use cases.

> It’s generally always a good idea to skim through the library's capabilities so that your brain
> remembers if capability **X** is something that you have already seen and just that act can help
> you with future use case

Let’s say you want to chain multiple assertions on a particular person from the same people response
that we have been looking at:

```json
[
    {
        "fname": "Kent",
        "lname": "Brockman",
        "person_id": 2,
        "timestamp": "2020-12-01T16:50:36.843495"
    },
    {
        "fname": "Bunny",
        "lname": "Easter",
        "person_id": 3,
        "timestamp": "2020-12-01T16:50:36.843706"
	}
	...
]
```

Remember we did the check of extracting the first names from available persons and then added a
check to see if `Kent` is contained in this:

```python
first_names = [people['fname'] for people in response_text]
assert_that(first_names).contains('Kent')
```

We can use capabilities offered by assertpy to extract a list from a **list** of **dict** objects
based on a certain key and then chain **multiple assertions** together. The above can be effectively
replaced with.

```python
assert_that(response_content).extracting('fname').is_not_empty().contains('Gaurav')
```

Observe that we are able to do multiple checks on the same object and this reads fluently like an
english sentence. 🙌🏼

Also, Notice when the assertion fails, we get a friendly human readable error message like below:

```zsh
AssertionError: Expected <['Kent', 'Bunny', 'Doug']> to contain item <Gaurav>, but did not.
```

Replace `Gaurav` with `Kent` to see the assertion pass.

The most common operations that you might perform with the assertion library are:

```zsh
is_equal_to, is_empty, contains, does_not_contain, matches
```

And these among many others are easily supported by assertpy out of the box.

## Printing a custom assertion message

Let’s say you want your own custom message to be printed when an assertion fails, You can easily do
that use `description=''` keyword argument

```python
assert_that(response.status_code, description='Person not created').is_equal_to(requests.codes.ok)
```

For example, I’ve wrongly modified the expected response code from `no_content` to `ok` and assertpy
gives the below readable stack trace along with our provided error message

```zsh
>       assert_that(response.status_code, description='Person not created').is_equal_to(requests.codes.ok)
E       AssertionError: [Person not created] Expected <204> to be equal to <200>, but was not.

people_test.py:63: AssertionError
```

## Soft assertions

You can also do **Soft assertions** (i.e not stop your test on the first failure) but instead raise
a single assertion error at the end, to do so, ensure that you make use of `soft_assertions()`
function and python context manager using `with` clause

```python
def test_read_all_has_kent():
   # We use requests.get() with url to make a get request
   response = requests.get(BASE_URI)
   # response from requests has many useful properties
   # we can assert on the response status code

   with soft_assertions():
       assert_that(response.status_code).is_equal_to(requests.codes.no_content) # fails
       # We can get python dict as response by using .json() method
       response_content = response.json()

       # Use assertpy's fluent assertions to extract all fnames and then see the result is non empty and has
       # Kent in it.
       assert_that(response_content).extracting('fname').is_not_empty().does_not_contain('Kent') # fails
```

In the above example, we’ve deliberately modified the status code assertion and the response
assertion.

Below is how it looks like once the test has run, we see both assertion messages show up.

```zsh
E           AssertionError: soft assertion failures:
E           1. Expected <200> to be equal to <204>, but was not.
E           2. Expected <['Kent', 'Bunny', 'Doug', 'New', 'New', 'New']> to not contain item <Kent>, but did.
```

## Conclusion

I hope you have a better sense of how a dedicated fluent assertion library makes your framework much
better and I hope you would use them going forwards. That's it for this post. We shall see how to
work with XML and JSON data types in the next posts in the series

If you found this post useful, Do share it with a friend or colleague and if you have thoughts, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing and Coding.
