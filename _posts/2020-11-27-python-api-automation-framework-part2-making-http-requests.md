---
title: Python API test automation framework (Part 2) Making HTTP requests
excerpt:
  "Learn how to make http requests in python using requests and pytest for a locally hosted Flask
  API"
layout: post
permalink: /2020/11/27/python-api-automation-framework-part2-making-http-requests
image: /assets/images/2020/11/api_course_header_2.png
categories:
  - "Test automation"
  - Testing
tags:
  - Python
---

![Python and requests and header](/assets/images/2020/11/api_course_header_2.png)

Logos in header image sources:
[Python](https://commons.wikimedia.org/wiki/File:Python-logo-notext.svg),
[Requests](https://en.wikipedia.org/wiki/File:Requests_Python_Logo.png),
[JSON](https://en.wikipedia.org/wiki/JSON),
[HTTP](https://commons.wikimedia.org/wiki/File:HTTP_logo.svg)

This is second post in a series on how to build an API framework using python.

Read part 1 [here]({% link
_posts/2020-11-23-python-api-automation-framework-part1-python-and-dependencies-setup.md %})

## Understanding API under test

Let’s understand the API that we will be using in this tutorial a bit better.

We will be using [people-api](https://github.com/automationhacks/people-api) which is a set of CRUD
HTTP operations developed using Python Flask, SQLAlchemy and uses sqlite as the database and
represents a list of persons with first name, last name and an id

To setup clone people-api repo from github and then activate the pipenv by running below:

```zsh
pipenv shell
```

Ensure all the dependencies are installed in the pipenv by executing:

```zsh
pipenv install
```

Once done, Init the database by executing

```zsh
python build_database.py
```

This would seed the local sqlite database with some dummy records

Finally then start the HTTP service on your local by executing and ensuring this keeps on running
during the test

```zsh
python server.py
```

We can see from the log that the local service has started, you would also see logs for any request
made to the server

```text
* Serving Flask app "config" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 105-008-664
```

Let’s navigate to `http://0.0.0.0:5000` to see the application,

> Note: To see the swagger spec for this API we can navigate to `http://0.0.0.0:5000/api/ui/#/`

As you can see this API supports basic CRUD operations (CREATE, READ, UPDATE, DELETE)

![Swagger preview](/assets/images/2020/11/swagger.png)

If you want to play around with these requests, I have also included a postman collection inside
this repo under `postman` folder with all these basic operations already setup.

The API supports creating a person, updating him/her, deleting the person and able to read a user or
all the users in the database. We will see these operations while writing tests.

## First test, read via GET API

Let’s see how we can create a basic test to make this HTTP request via python using `requests`
module that we have already imported

The curl for this API is:

```curl
curl --location --request GET 'http://0.0.0.0:5000//api/people' \
--header 'Accept: application/json'
```

Below is the code snippet that wires up a basic HTTP `GET` request and then asserts that the service
returns us a 200 status code and that the returned list of people has `kent` in it.

Notice we use `assert_that` from `assertpy` module for fluent assertions, The failure messages from
these are quite readable and we would discuss more about this in a future post. Please ensure you
have that installed in your virtualenv using `pipenv install assertpy`

```python
import requests
from assertpy.assertpy import assert_that
from config import BASE_URI

def test_read_all_has_kent():
    # We use requests.get() with url to make a get request
    response = requests.get(BASE_URI)
    # response from requests has many useful properties
    # we can assert on the response status code
    assert_that(response.status_code).is_equal_to(requests.codes.ok)
    # We can get python dict as response by using .json() method
    response_text = response.json()
    first_names = [people['fname'] for people in response_text]
    assert_that(first_names).contains('Kent')
```

In above, we are using `BASE_URI` variable to get the base api url to be used. This is stored in a
`config.py` file as below:

```python
BASE_URI = 'http://0.0.0.0:5000/api/people'
```

## Creating a person using POST method

Alright, now that we have the basic case of GET API taken care of, let’s see how we can make a POST
request.

Generally in Rest API’s when you need to create a resource you would use `POST` method

Below is the `cURL` to make the request, our python code is going to provide the same headers, body
and URL to hit the request

```curl
curl --location --request POST 'http://0.0.0.0:5000//api/people' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--data-raw '{
   "fname": "TAU",
   "lname": "User"
 }'
```

Here is the complete flow that we want to automate:

- Create a new person in the db
- Verify if the newly created user is present using the GET API
- Filter to find if the created data is present in all the users in the system

{% gist 3de97538503839ed2d681f4b63d1aef6 %}

Here Ln 2: `calls create_new_person()` where we first create the body to be passed as part of the
request

Notice on Ln 14 we are using `dumps()` method from `json` module to convert python dict to json
string (serialization) and using `str(uuid4())` to get a unique last name on Ln 13 to ensure we
don't have conflicting data on every test run

Finally we make the `POST` request using

```python
response = requests.post(url=BASE_URI, data=payload, headers=headers)
```

And then use `search_created_user_in()` method to see if the newly created user is present in the
database

## Deleting a person using DELETE method

How would we go about the delete method?

In this API we can delete a person by passing in the `person_id`, it is always a good practice to
create your own test data before trying delete operations instead of using any existing data since
that could result in non-deterministic tests

So here it the flow:

- Create a new person
- Get the person id using read API
- Hit the delete endpoint and assert

Since we already have methods to create and then read users, the only thing left is to implement the
DELETE operation by ensuring the `person_id` is passed in the API path params, We use the fantastic
`f-strings` to create our URL and then hit delete using `requests.delete()` method.

```python
def test_created_person_can_be_deleted():
    persons_last_name = create_new_person()

    peoples = requests.get(BASE_URI).json()
    newly_created_user = search_created_user_in(peoples, persons_last_name)[0]

    delete_url = f'{BASE_URI}/{newly_created_user["person_id"]}'
    response = requests.delete(delete_url)
    assert_that(response.status_code).is_equal_to(requests.codes.ok)
```

## Bonus

Note in assertions we are not specifying numeric value for the status codes, requests provides a
lookup dictionary wherein you can easily specify the code using readable english like syntax and
this is definitely better than parsing what code X means on
[MDN - Mozilla developer network](https://developer.mozilla.org/en-US/docs/Web/HTTP) every time 😉

In other words instead of `200` we could write it as `requests.codes.ok`

```python
assert_that(response.status_code).is_equal_to(requests.codes.ok)
```

## Conclusion

This is just a taste of what requests as a library can do. For more details on what all features it
provides please read [requests docs](https://requests.readthedocs.io/en/master/user/quickstart/) and
I hope this gives you a good idea on how to use requests to make HTTP calls. In the next post we
would discuss more on working with JSON/XML data types and assertions. Stay tuned. ⏰

And here are reads from MDN on
[Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) and
[Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) headers

If you found this post useful, Do share it with a friend or colleague and if you have thoughts, I'd
be more than happy to chat over at twitter or comments. Until next time. Happy Testing and Coding.
