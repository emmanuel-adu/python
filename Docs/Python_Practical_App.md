## Table of Content

- [Working with Files](#Working-with-Files)
- [Exceptions](#Exceptions)
- [Libraries and Modules](#Libraries-and-Modules)
- [Virtual Environment](#Virtual-Environment)

## Working with Files
### Open Files

Python provides a built-in function for opening files, cleverly titled `open()`. 
- The `open()` method will return an object that you can `read()` to get the data. 
- By default, `open()` will open a file in read-only mode, however you can change this by passing a mode parameter. 
- The list of optional modes is here:

|Character|Meaning|
|---|---|
|'r'|open for reading (default)|
|'w'|open for writing, truncating the file first|
|'x'|open for exclusive creation, failing if the file already exists|
|'a'|open for writing, appending to the end of the file if it exists|
|'b'|binary mode|
|'t'|text mode (default)|
|'+'|open a disk file for updating (reading and writing)|

Opening a file looks like this:

```python
# Open a file for reading
>>> my_file = open("my_file.txt")

# Open a file for reading or writing
# This will replace any existing file
>>> my_file = open("my_file.txt", "w")

# Open a file for reading or writing
# This will append to the end of any existing file
>>> my_file = open("my_file.txt", "a")
```

Of course, you always want to call `close()` on your open file object once you’re done with it, so that your program doesn’t leave open file handles dangling. 

But what happens if your program exits or crashes before you can close a file? You can use a `Context Manager`.

### Context Manager

A Context Manager is like a wrapper around a block of code that depends on some resource (*AKA file*). You can use a context manager to open a file in Python by using the `with` statement. The `with` statement provides a convenient way to handle resources, such as files, that require setup and cleanup actions.

- It’s a safer way of handling resources than, say, using `open()` and then remembering to `close()` later (and hoping your program doesn’t crash in between).
- It’s similar to using `try... finally`, but cleaner to look at.
- Context managers can contain code that auto-magically provisions a resource before your code runs, and cleans up afterward.
- For example, the `open()` function also works as a context manager, so opening a file looks like this:

```python
with open("filename.txt", "r") as file:
    contents = file.read()
    # work with the file contents

# file is automatically closed here
```

### Working with Files

```python
import json
with open("cities.json") as cities_file:
    cities_data = json.load(cities_file)
    print(cities_data)
# Let's pretty-print the results
from pprint import pprint
pprint(cities_data)
```

## Exceptions

Exceptions are a mechanism in Python for handling errors and exceptional situations in a program. They allow you to detect and respond to runtime errors in a controlled and predictable way, rather than letting them cause the program to crash.

### Types of Exceptions

Python has many useful built-in exceptions that you'll probably encounter in your travels. Some of the more common ones that you'll run into are:

|Exception|Cause of Error|
|---|---|
|AttributeError|Raised when an attribute assignment or reference fails.|
|ImportError|Raised when the imported module is not found.|
|IndexError|Raised when the index of a sequence is out of range.|
|KeyError|Raised when a key is not found in a dictionary.|
|KeyboardInterrupt|Raised when the user hits interrupt key (Ctrl+c or delete).|
|NameError|Raised when a variable is not found in local or global scope.|
|SyntaxError|Raised by parser when a syntax error is encountered.|
|IndentationError|Raised when there is incorrect indentation.|
|ValueError|Raised when a function gets an argument of correct type but improper value.|

You can find a more detailed list of built-in exceptions in the [Python documentation](https://docs.python.org/3/library/exceptions.html).

### The `except` Clause

```python
try:
	# Code to try
	d = {}
	d["a"]
	int("a")

except ValueError:
	# Code to run if there's a ValueError
	print("An exception happened.")

except KeyError:
	# Code to run if there's a KeyError
	print("A key was not found.")

print("End of the program.")
```

```shell
A key was not found.
End of the program.
```

### Finally

`finally` is an optional block that runs after `try`, `except`, regardless of if an exception is thrown or not. This is good for doing any cleanup that you want to happen, whether or not an exception is thrown.

```python
try:
    file = open("data.txt", "r")
    contents = file.read()
    x = int(input("Enter a number: "))
    print(contents / x)
except ZeroDivisionError:
    print("You cannot divide by zero.")
except Exception as e:
    print(f"An error occurred: {e}")
finally:
    file.close()
    print("File closed.")

```

### Custom Exceptions

```python
class InvalidInputError(Exception):
    def __init__(self, message):
        self.message = message

def validate_input(value):
    if value < 0:
        raise InvalidInputError("Input must be non-negative.")

try:
    value = int(input("Enter a number: "))
    validate_input(value)
except InvalidInputError as e:
    print(e.message)
```

## Libraries and Modules

### Main Method

In Python, the `main` method is a standard convention for creating a script that can be executed from the command line. The `main` method is defined as a function and serves as the entry point for the script.

- Used to write re-useable code by using `__name__ == __main__`
- `__name__` is a special variable that’s set by Python that tells it where it was called from.
- We can tell it’s a special variable because it starts and ends with `__`
	- That’s a hint that you don’t want to _change_ the value of this variable

```python
# name_lib.py

def name_length(name):
    return len(name)

def upper_case_name(name):
    return name.upper()

def lower_case_name(name):
    return name.lower()

# point at main
if __name__ == "__main__":
    name = "Nina"
    length = name_length(name)
    upper_case = upper_case_name(name)

    print(f"The length is {length} and the uppercase version is: {upper_case}")
```

```python
# other_program.py
import name_lib

my_name = "Fred"

my_length = name_lib.name_length(my_name)
my_lower_case = name_lib.lower_case_name(my_name)

print(f"In my code, my length is {my_length} and my lower case name is: {my_lower_case}")
```

>Using a `main` method is a common pattern that you’ll see in Python programs, and it comes in handy for being able to write programs that work both on their own and when imported into other programs.

## Virtual Environment

Virtual environments are a handy way to store the dependencies your Python application requires. Creating a virtual environment makes a self-contained folder that includes a full Python installation, allowing you to install dependencies specific to your application (or even a specific version of Python if you want) without relying on the global system version of Python.

### requirements.txt

`requirements.txt` is a special file that we use to tell `pip`, the Python package manager, which dependencies to install. The format is simple: you can create one manually by putting each dependency you import into a text file named `requirements.txt`, one dependency on each line.

1.  Create a `conda` environment for your project: 

```shell
conda create --name myenv
```

2.  Activate the environment:

```shell
conda activate myenv
```

3.  Install the required packages in the environment:

```shell
conda install numpy pandas matplotlib
# or with pip
(env) $ python -m pip install requests
```

4.  **Export the list of packages** and versions in the environment to a `requirements.txt` file:

```shell
conda list --explicit > requirements.txt
```

This will create a `requirements.txt` file in the current directory with the packages and versions installed in the `conda` environment. You can then use this file to recreate the environment and install the dependencies on other machines.

#### Exporting base dependencies

Exporting the base dependencies along with the packages in your `conda` environment is not as straightforward as exporting the packages, since base dependencies are typically installed outside the environment and are not managed by `conda`. However, there are a few different approaches that you can take to include the base dependencies in your `requirements.txt` file:

1. Manually specify the base dependencies: You can manually specify the base dependencies in the `requirements.txt` file along with the packages installed in the `conda` environment. For example, if you need to install the `Python` runtime and the `NumPy` library, you could add the following lines to your `requirements.txt` file:

```python
# requirements.txt
python=3.8
numpy
```

2.  Create a `conda` environment file: Another option is to create a `conda` environment file, which is a `YAML` file that describes the packages and versions in your environment. You can create a `conda` environment file using the `conda env export` command:

```shell
conda env export > environment.yml
```

This will create a `environment.yml` file that describes the packages, versions, and channels in your environment, including the base dependencies. You can then use this file to recreate the environment on another machine by using the `conda env create` command:

```shell
conda env create -f environment.yml
```

Note that while the `environment.yml` file will include the base dependencies, it may not be suitable for use with `pip`, since `pip` does not understand the `conda` package format. If you need to use `pip` to install the dependencies, you will need to use the `conda list --explicit` command to export the packages and versions in the `conda` environment to a `requirements.txt` file, as described in my previous answer.

#### Recreate Virtual Environment on other machine

To recreate the environment and install the dependencies on another machine, you can use the following steps:

1.  Install `conda` on the target machine if it's not already installed.
2.  Create a new `conda` environment based on the `requirements.txt` file:

```shell
conda create --name myenv --file requirements.txt
```

This will create a new `conda` environment named `myenv` and install the packages and versions specified in the `requirements.txt` file.

3.  Activate the environment:

```shell
conda activate myenv
```

4.  Verify that the required packages have been installed:

```shell
conda list
```

5. check env

```shell
conda env list
```
