---
title: Python API test automation framework (Part 5) Working with JSON and JsonPath
excerpt:
  "In this post, we explore how to perform serialization/de-serialization of JSON and use JsonPath
  to parse JSON strings which forms a crucial building block of any API test automation framework."
permalink: /2020/12/25/python-api-automation-framework-part5-working-with-json
image: /assets/images/2020/12/api_course_header_5.png
categories:
  - "Test automation"
  - Testing
tags:
  - Python
---

![Python and requests and header](/assets/images/2020/12/api_course_header_5.png)

Logos in header image sources:
[Python](https://commons.wikimedia.org/wiki/File:Python-logo-notext.svg),
[Requests](https://en.wikipedia.org/wiki/File:Requests_Python_Logo.png),
[JSON](https://en.wikipedia.org/wiki/JSON),
[HTTP](https://commons.wikimedia.org/wiki/File:HTTP_logo.svg)

This is fifth post in a series on how to build an API framework using python.

You can read previous parts below:

- [Python API test automation framework (Part 1) Introduction, Setup and Installation ]({% link
  _posts/2020-11-23-python-api-automation-framework-part1-python-and-dependencies-setup.md %})
- [Python API test automation framework (Part 2) Making HTTP requests]({% link
  _posts/2020-11-27-python-api-automation-framework-part2-making-http-requests.md %})
- [Python API test automation framework (Part 3) Writing Fluent assertions]({% link
  _posts/2020-12-07-python-api-automation-framework-part3-adding-fluent-assertions.md %})
- [Python API test automation framework (Part 4) Working with XML using LXML]({% link
  _posts/2020-12-17-python-api-automation-framework-part4-working-with-xml-using-lxml.md %})

---

JSON is one of the most common data format that is used for request and response payloads in API's
today and is very important to get a good grasp over.

If you are completely new to JSON format, please refer to the below sites to form an intuition of
what it is:

[JSON.org](https://www.json.org/json-en.html) or
[w3 schools](https://www.w3schools.com/whatis/whatis_json.asp)

I’ll try to give a quick summary here, it is mostly a `key: value` data structure with some
primitive data types like `string, boolean, numbers`, and an `array` data type and looks very
similar to a Python dictionary.

In fact, if you have already worked with nested dictionaries then you mostly understand JSON. 😉

Before we proceed, Let’s see some quick definitions that often come up when dealing with JSON format
for API automation

- The process of encoding a **Python object** to **JSON** is called **serialization**
- The process of converting a **JSON** to a **Python object** is called **de-serialization**

I know these terms appear similar and sometimes confusing, however, don’t worry you’ll get the hang
of it as you work with these more.

## Working with JSON

Python standard lib comes with out of the box support for JSON with the JSON module

There are primarily a couple of use cases that are often encountered

- Convert a python dict to JSON format to pass in the request
  - use `json.dump()` if you want to write to a file
  - or `json.dumps()` if you want to write to a python string
- Convert JSON to python dict
  - use `json.load()` if you want to read from a file directly
  - or `json.loads()` if you want to read from a python string

We’ve already seen the `json.dumps()` method in action in Chapter 2 and hence would not be going
into detail.

## Understanding a typical API test flow

Let’s say we want to automate the below scenario on our people api

- Read JSON from a file
  - (This could be useful if you want to store the request body as a template somewhere instead of
    having it specified in the tests or even a test data file)
- Modify some parameter in the request
- Convert the python dict into a JSON string
- Pass the JSON payload to the POST request to create a user using the people-api
- Get all the users in the current database using GET api
- Assert that the new user is created in the system using the JSON path instead of manual parsing

I’ve gone ahead and created a test for this. Let’s understand the different pieces:

### tests/data/create_person.json

```json
{
  "fname": "Sample firstname",
  "lname": "Sample lastname"
}}
```

Firstly, we have the `create_person.json` file under the **tests/data** directory to represent a
sample request body (often called request payload as well).

This is in general a good pattern to follow since this avoids you having to mention request bodies
explicitly in your tests and also makes your test files less bloated if you have a larger payload.

### utils/file_reader.py

```python
import json
from pathlib import Path

BASE_PATH = Path.cwd().joinpath('..', 'tests', 'data')


def read_file(file_name):
    path = get_file_with_json_extension(file_name)

    with path.open(mode='r') as f:
        return json.load(f)


def get_file_with_json_extension(file_name):
    if '.json' in file_name:
        path = BASE_PATH.joinpath(file_name)
    else:
        path = BASE_PATH.joinpath(f'{file_name}.json')
    return path
```

Next, we have `utils/file_reader.py` to give us a function that can accept a file name in the
tests/data directory, read it, and then send the JSON string back.

Couple of things to note here:

```python
with path.open(mode='r') as f:
    return json.load(f)
```

- Notice we are using the `path.open` instead of using pythons `open` method directly. This makes
  use of `Path` class from the [pathlib module](https://docs.python.org/3/library/pathlib.html) to
  easily help us build a file path (which is cross-platform out of the box) and use it easily.
- We also have a `get_file_with_json_extension` method which adds a `.json` extension if the file
  does not already have one.
- Also, we use `json.load()` and give it a file to read from directly and return a python object
  that we could

Alright, so this helps us get a python object.

### tests/people_test.py

Here is how we can use this in our test.

Below is the complete test file.

I know it looks huge 😏 Let’s unpack the changes.

```python
@pytest.fixture
def create_data():
    payload = read_file('create_person.json')

    random_no = random.randint(0, 1000)
    last_name = f'Olabini{random_no}'

    payload['lname'] = last_name
    yield payload


def test_person_can_be_added_with_a_json_template(create_data):
    create_person_with_unique_last_name(create_data)

    response = requests.get(BASE_URI)
    peoples = loads(response.text)

    # Get all last names for any object in the root array
    # Here $ = root, [*] represents any element in the array
    # Read full syntax: https://pypi.org/project/jsonpath-ng/
    jsonpath_expr = parse("$.[*].lname")
    result = [match.value for match in jsonpath_expr.find(peoples)]

    expected_last_name = create_data['lname']
    assert_that(result).contains(expected_last_name)


def create_person_with_unique_last_name(body=None):
    if body is None:
        # Ensure a user with a unique last name is created everytime the test runs
        # Note: json.dumps() is used to convert python dict to json string
        unique_last_name = f'User {str(uuid4())}'
        payload = dumps({
            'fname': 'New',
            'lname': unique_last_name
        })
    else:
        unique_last_name = body['lname']
        payload = dumps(body)

    # Setting default headers to show that the client accepts json
    # And will send json in the headers
    headers = {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
    }

    # We use requests.post method with keyword params to make the request more readable
    response = requests.post(url=BASE_URI, data=payload, headers=headers)
    assert_that(response.status_code, description='Person not created').is_equal_to(requests.codes.no_content)
    return unique_last_name
```

#### Make use of pytest fixture for data setup

```python
@pytest.fixture
def create_data():
    payload = read_file('create_person.json')

    random_no = random.randint(0, 1000)
    last_name = f'Olabini{random_no}'

    payload['lname'] = last_name
    yield payload
```

Above, instead of having the entire setup code in the test method. I’m making use of pytest fixtures
to inject the data into the tests. Note the fixture named `create_data` is passed as an argument to
test method `def test_person_can_be_added_with_a_json_template(create_data):`

We are getting the python dict as payload using `read_file('create_person.json')` and then using the
[random module](https://docs.python.org/3/library/random.html) to generate a random no between 0 and
1000 and then adding it to a prefix.

Finally, we update that in the request body and then provide it to the test method using the `yield`
keyword

We also modify the previously created `create_person_with_unique_last_name` to optionally take the
body in with a default value of None and use that to create JSON request body using the
`json.dumps()` method or if not provided, still retain previous functionality of generating the
request body.

## Using JSONPath

Finally, once our user is created let’s see how we can use a JSON path to extract values out of a
JSON

```python
# Get all last names for any object in the root array
# Here $ = root, [*] represents any element in the array
# Read full syntax: https://pypi.org/project/jsonpath-ng/
jsonpath_expr = parse("$.[*].lname")
result = [match.value for match in jsonpath_expr.find(peoples)]

expected_last_name = create_data['lname']
assert_that(result).contains(expected_last_name))
```

JSON path is a good way of working with a long nested JSON structure and it provides us XPath like
capabilities. To add this library to our framework, add below:

```python
pipenv install jsonpath-ng
```

For full details on the different use cases, this library can support refer to the PyPI page,
[jsonpath-ng](https://pypi.org/project/jsonpath-ng/)

### An example

For our case, let’s say we want to perform the same action that we did earlier. i.e. get all the
persons name and then check if the one that we expect is present inside the list.

We can specify the JSON path expression using the `parse("$.[*].lname")` method

The above expression translates to:

- `$` starting from the root,
- `[*]` for any element inside the array
- `.lname` get the value of keys named `lname`

To get this JSON path to execute we call the `find()` method and give it the response JSON from the
GET API response.

Finally, we assert that our expected last name is indeed present inside this list of users and fail
if not found.

## Conclusion

In this chapter, we saw,

- How can we serialize or deserialize JSON
- Manipulate it
- and, finally get enhanced JSON parsing capabilities.

Understanding how these concepts would serve you well to form the foundation of a successful API
test framework.

If you found this post useful, Do share it with a friend or colleague and if you have thoughts, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing.

You can find the complete code for this course on Github at
[automationhacks/course-api-framework-python](https://github.com/automationhacks/course-api-framework-python)

> And since this is going on on Christmas of 2020. Merry Christmas and happy holidays! 🎅 🎄 Enjoy

---

> [recruitment.com](https://recruitment.com/) has created a
> [list of the best freelance websites](https://recruitment.com/recommendations/hire-python-developers)
> to hire Python developers. It is also a helpful resource for those Python developers looking for
> their next freelance job opportunity. Feel free to check them out
