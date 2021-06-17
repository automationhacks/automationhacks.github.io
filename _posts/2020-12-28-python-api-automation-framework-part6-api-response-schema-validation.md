---
title: Python API test automation framework (Part 6) API response schema validation
excerpt:
  "Asserting that your api’s are returning responses conforming to valid schema contracts is very
  important. With a data validation library its often quite easy to add this additional coverage. We
  explore cerberus library towards that purpose in this post"
permalink: /2020/12/28/python-api-automation-framework-part6-api-response-schema-validation
image: /assets/images/2020/12/api_course_header_6.png
categories:
  - "Test automation"
  - Testing
tags:
  - Python
---

![Python and requests and header](/assets/images/2020/12/api_course_header_6.png)

Logos in header image sources:
[Python](https://commons.wikimedia.org/wiki/File:Python-logo-notext.svg),
[Requests](https://en.wikipedia.org/wiki/File:Requests_Python_Logo.png),
[JSON](https://en.wikipedia.org/wiki/JSON),
[HTTP](https://commons.wikimedia.org/wiki/File:HTTP_logo.svg),
[Cerberus](https://docs.python-cerberus.org/en/stable/_static/cerberus.png)

This is the sixth post in a series on how to build an API framework using python.

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

---

Most APIs return JSON that adhere to some contract set between its clients (could be another API or
a web app etc). While you can write consumer-driven contract tests, sometimes you might want to just
test with the live API and see if its response schema conforms to a fixed structure.

There are many different data validation libraries in the Python ecosystem and you can choose one
that meets your objectives. We will use
[Cerberus](https://docs.python-cerberus.org/en/stable/index.html) which is a quite popular library
for this purpose. Other notable libraries are [jsonschema](https://pypi.org/project/jsonschema/),
[voluptuous](https://pypi.org/project/voluptuous/) etc

## Setup

Install cerberus within your virtualenv

```zsh
pipenv install cerberus
```

## Schema test for Read operation in People API

Let’s say we want to check that our people API’s response conforms to a schema that we expect:

Below is the structure we get when we hit the read API

```json
{
	"fname": "Doug",
	"lname": "Farrell",
	"person_id": 1,
	"timestamp": "2020-12-01T16:50:36.842997"
}
```

Cerberus works by defining a schema with all the fields inside the response object and their types
and then validates if a sample response indeed met the schema need.

## Your first schema test

Below is a test to validate if Read one operation of people API meets a defined schema

```python
import json

import requests
from cerberus import Validator

from config import BASE_URI

schema = {
   "fname": {'type': 'string'},
   "lname": {'type': 'string'},
   "person_id": {'type': 'integer'},
   "timestamp": {'type': 'string'}
}


def test_read_one_operation_has_expected_schema():
   response = requests.get(f'{BASE_URI}/1')
   person = json.loads(response.text)

   validator = Validator(schema)
   is_valid = validator.validate(person)

   assert_that(is_valid, description=validator.errors).is_true()
```

Let’s understand how this is constructed.

We start with defining the expected schema of the response object, Since it is a single object with
certain keys like `fname, lname` etc, and values.

We can define a python dict with these schema details

```python
 "fname": {'type': 'string'}
```

Here for every field in the response, we specify key with the field name and value is another dict
specifying the type like string, number, boolean, date etc.

> See the full list of types on
> [cerberus docs](https://docs.python-cerberus.org/en/stable/validation-rules.html#type)

Sweet, Below is how the schema looks like for the read response

```python
schema = {
   "fname": {'type': 'string'},
   "lname": {'type': 'string'},
   "person_id": {'type': 'integer'},
   "timestamp": {'type': 'string'}
}
```

We then hit the GET API with an expected person id and then convert the response to a python dict
using loads()

```python
response = requests.get(f'{BASE_URI}/1')
person = json.loads(response.text)
```

> Note: Hard coding a user id like 1 (in the request URL) is often something to be avoided. You
> might want to create a new user and then do this test, however since this API gets seeded with
> some dummy data, we are following this approach for demo purposes only.

We then initialize an instance of `Validator` class with this schema. Optionally, if we want to
specify that all the keys are required in this schema then we can add `require_all=True` keyword
argument. Or we could even specify this at a field level using `'required': True/False` in the
schema itself.

```python
validator = Validator(schema, require_all=True)
```

We can assess if the JSON matches this schema with below:

```python
is_valid = validator.validate(person)
```

And if we want to raise an assertion error if Cerberus finds a mismatch then we can print
`validator.errors`

```python
assert_that(is_valid, description=validator.errors).is_true()
```

When we run the test for our current people API, we see the test passes.

To see how it would look like in case of a failure we can change the type of `person_id` from
`number` to `string` and that would raise the error message below, notice we get to know the field
that is mismatched and what the validation failure is.

```text
AssertionError: [{'person_id': ['must be of string type']}] Expected <True>, but was not.
```

## Test for read all operation

How does this test look like for the Read all operation?

```python
def test_read_all_operation_has_expected_schema():
   response = requests.get(BASE_URI)
   persons = json.loads(response.text)

   validator = Validator(schema, require_all=True)

   with soft_assertions():
       for person in persons:
           is_valid = validator.validate(person)
           assert_that(is_valid, description=validator.errors).is_true()
```

Essentially, We get the list of persons and then repeat the same validation for all the records in
this list while wrapping it with a soft assertion to ensure all the validation failures are
collected and printed in the end.

## Conclusion

Schema validation is an important component to include in your API automation framework and I hope
you have a basic understanding of how to use a tool like Cerberus to achieve this. For
understanding, all the nuances of this approach feel free to dig deep into Cerberus docs which lists
a lot of the functionality that is available.

You can find the complete code for this course on Github at
[automationhacks/course-api-framework-python](https://github.com/automationhacks/course-api-framework-python)

If you found this post useful, Do share it with a friend or colleague and if you have thoughts, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing.

Further reads:

- [Cerberus project docs](https://docs.python-cerberus.org/en/stable/index.html)
- [Understanding Validation schemas](https://docs.python-cerberus.org/en/stable/schemas.html)
- [require_all](https://docs.python-cerberus.org/en/stable/usage.html#requiring-all)
