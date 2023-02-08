Working with external libraries in Python makes use of the `import` keyword. While this can go anywhere in your file, it’s almost always best to import libraries at the top of each file where they’re used.

## Table of Contents

- [[#Libraries|Libraries]]
- [[#Modules|Modules]]
- [[#Tests|Tests]]
- [[#Request Library|Request Library]]

## Libraries

- Importing modules with the `import` keyword
- you can also use the `from <module> import <object>` syntax to import a specific object (function, variable, subclass, etc.)

 `random.randint()`:

```python
# Import the entire module
import random 
random.randint(0, 100)

# We can check whats in the module and what it does
>>> dir(random)
>>> help(random.randint) 

# Import a method from the module
from random import randint
randint(0, 100)
64
```

### Standard Library

Python has a rich and versatile standard library which is immediately available, without making the user download separate packages.

- The full list of standard libraries can be found in the [Python documentation](https://docs.python.org/3/library/).

## Modules

Python has a simple package structure. Any directory with a file named `__init__.py` can be considered a Python module.

>Note: a `__init__.py` file is no longer _required_ for Python 3 modules, but it’s still supported and can be useful.

For example, let’s make a basic function and start a new module to house it:

```python 
def add_numbers(x, y):
    return x + y
```

Let’s put our function in a file called `__init__.py` and place it in a folder called `my_math_functions`. 

```shell
my_math_functions
└── __init__.py
```

- Now, as long as the folder `my_math_functions` is somewhere in our `PYTHONPATH`, we can `import my_math_functions` and reach `add_numbers()`.

**import function from module**

```python
# from other file
from my_math_functions import add_numbers
add_numbers(1, 2)
```

>You can use the `as` keyword to make things a little easier on yourself.

```python
>>> import my_math_functions as mmf # can you as 
>>> mmf.add_numbers(1, 2)
3
```

## Tests

### Assert

Python comes with a handy-dandy `assert` keyword that you can use for simple sanity checks. An assertion is simply a boolean expression that checks if its conditions return true or not.

-  If the assertion is true, the program continues. If it’s false, it throws an `AssertionError`, and your program will stop.
- `assert` is for Sanity Checks, not for production!

```python
input_value = 25
assert input_value > 0
```

### Writing your Tests

There are a few different frameworks for writing unit tests in Python, but they’re all very similar.
- We’ll focus on the built-in `unittest` library.

In order to write `unittest` tests, you must:
- Write your tests as methods within classes
- Use a series of built-in assertion methods

```python
import unittest
import my_math_functions as mmf 

class TestAddition(unittest.TestCase):

    def test_addition(self):
        test_x = 5
        test_y = 10
        self.assertEqual(mmf.add_numbers(test_x, test_y), 15, "Should be 15")

if __name__ == "__main__":
    unittest.main()
    ```

### Important Concepts

-   `TestCase` class must subclass `unittest.TestCase`
-   Names of test functions must begin with `test_`
-   Import the code to be tested

Lastly, your test code will need access to your code to be tested. For a small project, this is easily done by putting your tests in a `test.py` file alongside your code. For larger projects, you usually want to have multiple test files inside a `test` folder.

### TestCase Assertions

Subclassing the TestCase class gives you a bunch of useful assertions that you can use to check the validity of your code. Here's the list from the [Python documentation](https://docs.python.org/3/library/unittest.html):


|Method|Checks that|
|---|---|
|assertEqual(a, b)|a == b|
|assertNotEqual(a, b)|a != b|
|assertTrue(x)|bool(x) is True|
|assertFalse(x)|bool(x) is False|
|assertIs(a, b)|a is b|
|assertIsNot(a, b)|a is not b|
|assertIsNone(x)|x is None|
|assertIsNotNone(x)|x is not None|
|assertIn(a, b)|a in b|
|assertNotIn(a, b)|a not in b|
|assertIsInstance(a, b)|isinstance(a, b)|
|assertNotIsInstance(a, b)|not isinstance(a, b)|

### Growing your tests

Standard `unittest` tests are fine for most projects. As your programs grow and organization becomes more complex, you might want to consider an alternative testing framework or test runner. The 3rd party `nose2` and `pytest` modules are compatible with `unittest` but do things slightly differently. You can find more information in the [nose2 documentation](https://nose2.readthedocs.io/en/latest/) and [pytest documentation](https://docs.pytest.org/en/latest/).

## External Packages

PyPI (the Python Package Index) is an awesome service that helps you find and install software developed and shared by the Python community.

- You can browse the site at [pypi.org](https://pypi.org/) but most of the time you will probably interact with it through Python’s `pip` tool.

```bash
(env) $ python -m pip install SomePackage
```

### Know your Packages

Sometimes it helps to look at a package before installing it. Simply search for a package name on PyPI.org - for example, here’s the page for the [redis package](https://pypi.org/project/redis/). If you follow the Homepage link, you’ll be taken to the project’s [GitHub page](https://github.com/andymccurdy/redis-py), where you can see that the latest commit was very recently.

You can use the `pip` tool to install the latest version of a module and its dependencies from the Python Packaging Index:

## Request Library

The external `requests` library was developed by Kenneth Reitz to make working with APIs in Python a lot easier. He calls it “HTTP, for humans.”

```python
import requests

# Define a variable with the URL of the API
api_url = "http://shibe.online/api/shibes?count=1"

# Call the root of the api with GET, store the answer in a response variable
# This call will return a list of URLs that represent dog pictures
response = requests.get(api_url)


# Get the status code for the response. Should be 200 OK
# Which means everything worked as expected
print(f"Response status code is: {response.status_code}")

# Get the result as JSON
response_json = response.json()

# Print it. We should see a list with one image URL.
print(response_json)

# Passing in a non-existant URL will result in a 404 (not found)
bad_response = requests.get("http://shibe.online/api/german-shepards")

print(f"Bad Response Status Code is: {bad_response.status_code}") # Status code is 404, meaning that resource doesn’t exist.
```

https://requests.readthedocs.io/en/latest/user/quickstart/
