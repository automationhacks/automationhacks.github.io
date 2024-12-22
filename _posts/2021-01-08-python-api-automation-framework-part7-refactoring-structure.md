---
title: Python API test automation framework (Part 7) Refactoring structure
excerpt:
  "So far we've seen how to do something using a specific module in python and their syntaxes. In
  this post we explore what could be a good API automation framework structure and refactor our
  existing tests into just that."
permalink: /2021/01/08/python-api-automation-framework-part7-refactoring-structure
image: /assets/images/2021/01/api_course_header_7.png
categories:
  - "Backend automation"
tags:
  - "Python"
  - "API testing"
---

![Python and requests and header](/assets/images/2021/01/api_course_header_7.png)

Logos in header image sources:
[Python](https://commons.wikimedia.org/wiki/File:Python-logo-notext.svg),
[Requests](https://en.wikipedia.org/wiki/File:Requests_Python_Logo.png),
[JSON](https://en.wikipedia.org/wiki/JSON),
[HTTP](https://commons.wikimedia.org/wiki/File:HTTP_logo.svg),
[Cerberus](https://docs.python-cerberus.org/en/stable/_static/cerberus.png)

This is the seventh post in a series on how to build an API framework using python.

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

---

So far, we’ve been observing how to achieve a specific piece of functionality in our API framework
using available packages in the python ecosystem.

However, when we talk about a framework, we have to do a bit more upfront thinking about how this
would be used by team members and the overall structure in which it is organized becomes as
important as well.

> One way that I typically approach is to decide on an structure based on initial needs and then
> continuously refactor as the domain, context changes, typically after a few cycles the structure
> and the relationships between different modules, classes becomes clear and you have your framework
> structure.

Let’s see what some of these changes are:

## Remove unnecessary comment and replace them with well named functions/classes

If you have been following along earlier commits/posts in this series, you would have seen that we
had given `inline comments` using `#` above many lines of code.

While this might be okay for a demo framework like this, I still wanted to call out that this
practice could be quite bad in a real project. Reason being, with every passing wave of refactoring
you might extract certain functions or rename variables or even change behavior in some cases.

Quite often, it's easy to forget updating the comment and then you have comments which don’t even
match with underlying logic and that is just plain confusing for the person who reads your code. 🤷🏼‍♂️

I’ve thus removed these from this branch and from the final master branch as well.

Below is the updated tests file with this and some other changes:

`tests/people_test.py`

```python
import random
from json import loads

import pytest
import requests
from assertpy.assertpy import assert_that
from jsonpath_ng import parse

from clients.people.people_client import PeopleClient
from config import BASE_URI
from tests.helpers.people_helpers import search_created_user_in
from utils.file_reader import read_file

client = PeopleClient()


def test_read_all_has_kent():
   response = client.read_all_persons()

   assert_that(response.status_code).is_equal_to(requests.codes.ok)
   assert_that(response.as_dict).extracting('fname').is_not_empty().contains('Kent')


def test_new_person_can_be_added():
   last_name, response = client.create_person()
   peoples = client.read_all_persons().as_dict

   is_new_user_created = search_created_user_in(peoples, last_name)
   assert_that(is_new_user_created).is_not_empty()
```

Notice, we have replaced all the comments with better named functions that clarify intent.

## Introducing client class as an abstraction layer

In earlier posts, we were directly calling `requests.get()`, `post()` and other methods and working
with response objects.

This is often a practice to avoid because it tightly couples our test implementation to request
libraries implementation

While requests (or, any other library) today does a good job for us, we might have to tweak its
behavior for all our tests or might have to switch to a different library altogether.

To ensure minimal changes to test code in those scenarios, it's always a good idea to wrap these
third party library code into an abstraction that we maintain.

One common pattern is to **abstract these domain operations into their own client class/module.**

I’ve thus introduced a people_client.py

`clients/people/people_client.py`

```python
from json import dumps
from uuid import uuid4

from clients.people.base_client import BaseClient
from config import BASE_URI
from utils.request import APIRequest


class PeopleClient(BaseClient):
   def __init__(self):
       super().__init__()

       self.base_url = BASE_URI
       self.request = APIRequest()

   def create_person(self, body=None):
       last_name, response = self.__create_person_with_unique_last_name(body)
       return last_name, response

   def __create_person_with_unique_last_name(self, body=None):
       if body is None:
           last_name = f'User {str(uuid4())}'
           payload = dumps({
               'fname': 'New',
               'lname': last_name
           })
       else:
           last_name = body['lname']
           payload = dumps(body)

       response = self.request.post(self.base_url, payload, self.headers)
       return last_name, response

   def read_one_person_by_id(self, person_id):
       pass

   def read_all_persons(self):
       return self.request.get(self.base_url)

   def update_person(self):
       pass

   def delete_person(self, person_id):
       url = f'{BASE_URI}/{person_id}'
       return self.request.delete(url)
```

Notice this has simple wrapper methods for the same operations that we were directly calling from
the test function and also makes every call to requests from an object of `APIRequest()` class
instead of calling request module directly

How does this APIRequest class look like?

`utils/request.py`

```python
from dataclasses import dataclass

import requests


@dataclass
class Response:
   status_code: int
   text: str
   as_dict: object
   headers: dict


class APIRequest:
   def get(self, url):
       response = requests.get(url)
       return self.__get_responses(response)

   def post(self, url, payload, headers):
       response = requests.post(url, data=payload, headers=headers)
       return self.__get_responses(response)

   def delete(self, url):
       response = requests.delete(url)
       return self.__get_responses(response)

   def __get_responses(self, response):
       status_code = response.status_code
       text = response.text

       try:
           as_dict = response.json()
       except Exception:
           as_dict = {}

       headers = response.headers

       return Response(
           status_code, text, as_dict, headers
       )
```

Notice, we have created wrapper methods for the **HTTP operations** that our current framework
needs, namely **post(), delete()** and also we are wrapping the response object into a custom object
that we control.

This is very powerful for the above mentioned reasons

- We can now easily modify request libraries behavior without changing underlying tests
- Our clients are not depending on requests library and we are free to switch to a different
  implementation in the future if such a need arises.

We also make use of Pythons [`@dataclass`](https://realpython.com/python-data-classes/) annotation
to create this data holder and use the private method `__get_responses` to take a response object
from requests and then return our own implementation.

### Make the client thin

Another thing to observe is, we have not put any validations on **response status code, body,
headers** in these client methods.

This is intentional since we want this to be the tests concern. The client just gives a simple class
to make these HTTP requests and leaves all implementation details for different validations to the
tests.

This approach ensures we can reuse the same method in the client to test for a **success (2XX) or a
failure case (4XX, 5XX)** status code.

## Abstract helper methods into their own class/module

I’ve also moved some helper methods related to searching a person in response and the JSON path
implementation into its own module, this ensures that the test code is clean and there is less
cognitive overload on the person looking at the code to grasp each and every detail.

For instance a descriptive method name like `search_created_user_in` is always going to be more
understandable than `[person for person in peoples if person['lname'] == last_name][0]` which
requires the code reader to grasp python list comprehension, array slicing and what not.

`tests/helpers/people_helpers.py`

```python
from jsonpath_ng import parse


def search_created_user_in(peoples, last_name):
   return [person for person in peoples if person['lname'] == last_name][0]


def search_nodes_using_json_path(peoples, json_path):
   jsonpath_expr = parse(json_path)
   return [match.value for match in jsonpath_expr.find(peoples)]
```

## Abstract common assertions into their own module

I’ve also extracted some assertions into their own functions and moved them into their own module,
for above reasons

`tests/assertions/people_assertions.py`

```python
from assertpy import assert_that


def assert_people_have_person_with_first_name(response, first_name):
   assert_that(response.as_dict).extracting('fname').is_not_empty().contains(first_name)


def assert_person_is_present(is_new_user_created):
   assert_that(is_new_user_created).is_not_empty()
```

## Extract fixtures into `conftest.py` file

Pytest framework has the flexibility to put
[fixture code into a `conftest.py`](https://stackoverflow.com/questions/34466027/in-pytest-what-is-the-use-of-conftest-py-files)
file which is auto discovered and allows us to separate setup teardown code from the actual tests.

These fixtures can be reused at different levels and you can easily move them up the directory
structure if you want the same fixtures to be available to many different test files

`tests/conftest.py`

```python
import random

import pytest

from utils.file_reader import read_file


@pytest.fixture
def create_data():
   payload = read_file('create_person.json')

   random_no = random.randint(0, 1000)
   last_name = f'Olabini{random_no}'

   payload['lname'] = last_name
   yield payload
```

In the end our entire test file is now well refactored and much more readable.

```python
import requests

from clients.people.people_client import PeopleClient
from tests.assertions.people_assertions import *
from tests.helpers.people_helpers import *

client = PeopleClient()


def test_read_all_has_kent():
   response = client.read_all_persons()

   assert_that(response.status_code).is_equal_to(requests.codes.ok)
   assert_people_have_person_with_first_name(response, first_name='Kent')


def test_new_person_can_be_added():
   last_name, response = client.create_person()
   assert_that(response.status_code, description='Person not created').is_equal_to(requests.codes.no_content)

   peoples = client.read_all_persons().as_dict
   is_new_user_created = search_created_user_in(peoples, last_name)
   assert_person_is_present(is_new_user_created)


def test_created_person_can_be_deleted():
   persons_last_name, _ = client.create_person()

   peoples = client.read_all_persons().as_dict
   new_person_id = search_created_user_in(peoples, persons_last_name)['person_id']

   response = client.delete_person(new_person_id)
   assert_that(response.status_code).is_equal_to(requests.codes.ok)


def test_person_can_be_added_with_a_json_template(create_data):
   client.create_person(create_data)

   response = client.read_all_persons()
   peoples = response.as_dict

   result = search_nodes_using_json_path(peoples, json_path="$.[*].lname")

   expected_last_name = create_data['lname']
   assert_that(result).contains(expected_last_name)
```

## A Simple heuristic to follow: Make it work => beautiful => fast

Notice how we approached this whole exercise and did these refactoring in phases. That is one
iterative way to build frameworks and has the benefit of ensuring only the required bits of code
come into the framework.

Below is the general heuristic i follow which has been written about multiple times.

- **Make it work**: Write the simplest thing possible that could work and get the job done first,
  don't do any [premature optimizations](http://wiki.c2.com/?PrematureOptimization) in this phase
- **Make it beautiful**: With implementation details figured out, think of how you can structure it
  better and refactor existing lines of code, methods into their own logical place. This is where
  you think of patterns, structure, which responsibilities lie with which class/module etc.
- **Make it fast**: Make the code you write something that runs really fast. In this phase, You
  optimize your implementation (after profiling current performance) and think about concurrency as
  well. More on this in a future post.

## Conclusion

In summary, Most of the concerns were abstracted into a dedicated place which can be easily
understood and modified in the future.

Is this the perfect structure though?

Heck no 🥴, what you decide on heavily maps to your specific domain models and context, however
treat these as some guidelines along the way on how to approach structuring your framework.

A well defined structure would most often than not, **stand the test of time** while ensuring all
the people contributing understand and are able to navigate it with ease and is a very important
aspect that good software engineers care about.

You can see this entire code on
[this Github repo and branch](https://github.com/automationhacks/course-api-framework-python/tree/example/07_refactoring_structure)

If you found this post useful, Do share it with a friend or colleague and if you have thoughts, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing.
