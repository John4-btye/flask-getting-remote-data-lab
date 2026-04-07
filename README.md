# Getting Remote Data Lab

## The Scenario

It is time to practice building out your own class for retrieving remote data. In this lab, you are tasked with building a generic GetRequester class. This class will be able to take in a URL on initialization and send an HTTP GET request on command. You will also need to build a method for dealing with requests that return JSON.

## Tools and Resources

- [GitHub Repo](https://github.com/learn-co-curriculum/flask-getting-remote-data-lab)
- [GET - Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)
- [HTTP methods - Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [requests](https://requests.readthedocs.io/en/latest/)
- [Python JSON](https://docs.python.org/3/library/json.html)

## Instructions

### Set Up

Before we begin coding, let's complete the initial setup for this lesson:

- Fork and Clone
  - For this lesson, you will need the following GitHub Repo:
  - Go to the provided GitHub repository link.
  - Fork the repository to your GitHub account.
  - Clone the forked repository to your local machine.
- Open and Run File
  - Open the project in VSCode.
  - Run pipenv install to install all necessary dependencies.
  - Run pipenv shell to open instance of python shell

### Task 1: Define the Problem

- Build a class to interact with api
- Get the data
- Convert to json data

### Task 2: Determine the Design

- Endpoint: https://learn-co-curriculum.github.io/json-site-example/endpoints/people.json.
  - `get_response_body`
    - Query endpoint
  - `load_json`
    - Convert to json data

#### Task 3: Develop, Test, and Refine the Code

- Create feature branch
- Build get_response_body to query endpoint
- Convert endpoint data to json and return the data
- Push feature branch and open a PR on GitHub
- Merge to main

#### Task 4: Document and Maintain

Best Practice documentation steps:

- Add comments to code to explain purpose and logic, clarifying intent / functionality of code to other developers.
- Add screenshot of completed work included in Markdown in README.
- Update README text to reflect the functionality of the application following https://makeareadme.com.
- Delete any stale branches on GitHub
- Remove unnecessary/commented out code
- If needed, update git ignore to remove sensitive data

## Submission

Once all tests are passing and working code is pushed to the GitHub main branch, submit your GitHub repo through Canvas using CodeGrade.

## Grading Criteria

The application passes all test suites.

- Get json data
- Convert to Json

# Flask Remote Data Retrieval Lab

## Overview

This project introduces a reusable class, `GetRequester`, designed to retrieve and process remote JSON data. The goal is to simulate how a Flask application can dynamically consume external API data—in this case, an employee directory—and make it available for rendering in templates.

---

## What Was Implemented

### 1. `GetRequester` Class

A custom class was created to handle HTTP GET requests and JSON parsing.

#### Responsibilities:

- Accept a URL during initialization
- Send a GET request to the provided endpoint
- Return the raw response data
- Convert the response into usable Python data structures

---

### 2. `get_response_body` Method

This method:

- Sends an HTTP GET request to the provided URL
- Returns the **raw response body as bytes**

```python
def get_response_body(self):
    response = requests.get(self.url)
    return response.content
```

#### Key Detail:

- `.content` is used instead of `.text` because the tests expect **byte-formatted data**

---

### 3. `load_json` Method

This method:

- Calls `get_response_body()` to retrieve the raw response
- Converts the JSON data into Python objects using `json.loads`

```python
def load_json(self):
    body = self.get_response_body()
    return json.loads(body)
```

#### Output:

- Returns a Python list of dictionaries representing employee data

---

## Example Data Source

The application retrieves data from the following endpoint:

```
https://learn-co-curriculum.github.io/json-site-example/endpoints/people.json
```

This endpoint returns a JSON array of employee records, including names and occupations.

---

## How It Works

1. A `GetRequester` instance is created with a target URL
2. `get_response_body()` fetches the raw data
3. `load_json()` parses that data into Python structures
4. The data can then be used in a Flask route and passed into templates

---

## Key Improvements Made

- Implemented HTTP GET functionality using `requests`
- Ensured compatibility with tests by returning **byte data**
- Eliminated redundant API calls by reusing `get_response_body()` in `load_json()`
- Added clear method separation for maintainability
- Structured code for reuse in future Flask applications

---

## Testing

All functionality was verified using `pytest`.

### Result:

```
2 passed
```

Tests confirm:

- Correct retrieval of raw response data
- Proper conversion of JSON into Python objects

---

## Best Practices Applied

- Separation of concerns (request vs parsing)
- Reusable class design
- Clean and readable code structure
- Minimal redundancy (DRY principle)
- Proper use of Python standard libraries

---

## Conclusion

This project demonstrates how to build a foundational API consumption layer that can be integrated into any Flask application. The `GetRequester` class provides a clean and reusable approach to retrieving and handling remote JSON data.
