## Table of Content

- [Python REPL](#Python-REPL)
- [Mutability](#Mutability)
- [Common Data Types](#Common-Data-Types)
- [Data Types](#Data-Types)
- [Functions](#Functions)
- [Boolean Logic](#Boolean-Logic)
- [if Statement and Conditionals](#`if`-Statement-and-Conditionals)
- [Loops](#Loops)
- [Comprehensions](#Comprehensions)
- [Slicing](#Slicing)

## Python REPL

Official docs: https://practical.learnpython.dev/

Install Python - www.anaconda.com/downloads
Helpful REPL methods
- `help(class.method)` - get description of class or method
- `type(value or variable)` - return type
- `dir(class)` - show available methods in the class. *Ignore methods with underscore*
- exit - `ctr + d`
- VS Code - `cmd + shift + p` then type python:start REPL

### Running .py files

For optimization and other reasons, Python code can be compiled to intermediary `.pyc` files.
- To safely delete them from the current project directory, run `find . -name "*.pyc" -delete`
- Pretty Printing with `pprint`

## Mutability

The fundamental distinction that Python makes on data is whether or not the value of an object changes. An object is mutable if the value can change; else, the object is _immutable_.

### Simple Types
All of the simple data types we covered first are **immutable**. 
- You can replace the value, but you can't change it.

| type                      	| use                     	| mutable? 	|
|---------------------------	|-------------------------	|----------	|
| `int`, `float`, `decimal` 	| store numbers           	| **no**   	|
| `str`                     	| store strings           	| **no**   	|
| `bool`                    	| store `True` or `False` 	| **no**   	|

### Container Types

For the mutability of the container types we covered next, check this helpful list:

| container type | use                                                                                                                               | mutable? |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------- | -------- |
| `list`         | ordered group of items, accessible by position                                                                                    | **yes**  |
| `set`          | mutable unordered group consisting only of immutable items. useful for set operations (membership, intersection, difference, etc) | **yes**  |
| `tuple`        | immutable collection containing ordered groups of items                                                                           | **no**   |
| `dict`         | contains key value pairs                                                                                                          | **yes**  |

![](../Attachments/Pasted%20image%2020230130174041.png)

## Common Data Types

Everything value type in python is a class
- Common Math methods: `min`, `max`, `round`
- long string use triple quote and press enter: `""" long string """`
- No value is `None`
- Boolean: `True` and `False`
- *f string* string formatting. This is the best method
```python
name = "Nina"
greeting = f"Hello, {name}"
print(greeting)
```

## Data Types

![](../Attachments/Pasted%20image%2020230129232143.png)

### List 

`len(list_variable_name)` check length of a list
- method on list does not change the original variable type but method.list does
```python
# Various ways to create a list
list1=[1,4,"Gitam",6,"college"]
list2=[] # creates an empty list
list3=list((1,2,3))

# Original variable is unchanged
lottery_numbers = [1, 4, 32423, 2, 45, 11]
sorted(lottery_numbers)
[1, 2, 4, 11, 45, 32423]
lottery_numbers
[1, 4, 32423, 2, 45, 11]
sorted(lottery_numbers, reverse=True)
lottery_numbers
[1, 4, 32423, 2, 45, 11]

# Original varaible is changed
lottery_numbers = [1, 4, 32423, 2, 45, 11]
lottery_numbers.sort()
lottery_numbers
[1, 2, 4, 11, 45, 32423]
lottery_numbers.sort(reverse=True)
lottery_numbers
words = ["Umbrella", "Fox", "Apple"]
words.sort()
words
```
- You can find items in a list with `in`
```python
"Nina" in names 
True 
"Rose" in names 
False
```

- Update  a list: 
	- `my_list.index(item)`
	- `my_list[pos] = new_item`

Lists are one of the most powerful data types in Python. They're used to store related items together.

#### `list` cheat sheet

| type               | `list`                                                                                                                                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| use                | Used for storing similar items, and in cases where items need to be added or removed.                                                                                                                  |
| creation           | `[]` or `list()` for empty list, or `[1, 2, 3]` for a list with items.                                                                                                                                 |
| search methods     | `my_list.index(item)` or `item in my_list`                                                                                                                                                             |
| search speed       | Searching for an item in a large list is slow because each item must be checked.                                                                                                                       |
| common methods     | `len(my_list)`, `append(item)` to add, `insert(index, item)` to insert at `index`, `pop()` to remove.                                                                                                  |
| order preserved?   | Yes. Items can be accessed by index.                                                                                                                                                                   |
| mutable?           | Yes                                                                                                                                                                                                    |
| in-place sortable? | Yes. `my_list.sort()` will sort the list in-place. `my_list.sort(reverse=True)` will sort the list in-place in *descending* order. `my_list.reverse()` will *reverse the items* in `my_list` in-place. |

#### Adding, Removing, Changing, and Finding Items in `list`s cheat sheet

| action                                           | method                                | returns           | possible errors                            |
| ------------------------------------------------ | ------------------------------------- | ----------------- | ------------------------------------------ |
| check length                                     | `len(my_list)`                        | `int`             |                                            |
| **add:** to the end                              | `my_list.append(item)`                | -                 |                                            |
| **insert:** at position                          | `my_list.insert(pos, item)`           | -                 |                                            |
| **update:** at position                          | `my_list[pos] = item`                 | -        -        | `IndexError` if `pos` is >= `len(my_list)` |
| **extend:** add items from another list          | `my_list.extend(other_list)`          | -                 |                                            |
| is item in list?                                 | `item in my_list`                     | `True` or `False` |                                            |
| **index** of item                                | `my_list.index(item)`                 | `int`             | `ValueError` if `item` is not in `my_list` |
| **count** of item                                | `my_list.count(item)`                 | `int`             |                                            |
| **remove** an item                               | `my_list.remove(item)`                | -                 | `ValueError` if `item` not in `my_list`    |
| **remove** the last item, or an item at an index | `my_list.pop()` or `my_list.pop(pos)` | `item`            | `IndexError` if `pos` >= `len(my_list)`    |

### Tuples

You might ask, why `tuple` when Python already has lists? `tuple` is different in a few ways. 
- While lists are generally used to store collections of similar items together, `tuple`s, by contrast, can be used to contain a snapshot of data. 
- A good use of a `tuple` might be for storing the information for a _row_ in a spreadsheet. 
- We don’t necessarily care about updating or manipulating that data, we just want a read-only snapshot. 
- *For data that will remain unchanged*
- *immutable*

```python
# Various ways to create tuples
tuple1=(1,2,"college",9)
tuple2=() # creates an empty tuple
tuple3=tuple((1,3,5,9,"hello"))
```

| type               | `tuple`                                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------------------- |
| use                | Used for storing a snapshot of related items when we don't plan on modifying, adding, or removing data. |
| creation           | `()` or `tuple()` for empty tuple. `(1, )` for one item, or `(1, 2, 3)` for a tuple with several items. |
| search methods     | `my_tuple.index(item)` or `item in my_tuple`                                                            |
| search speed       | Searching for an item in a large tuple is slow. Each item must be checked.                              |
| common methods     | Can't add or remove from tuples.                                                                        |
| order preserved?   | Yes. Items can be accessed by index.                                                                    |
| mutable?           | **No**                                                                                                  |
| in-place sortable? | **No**                                                                                                  |

#### Gotcha

```python
# Tupple should have a trailing comma
b = (1)
type(b)
<class 'int'>

# trailing comma added
c = (1, )
type(c) 
<class 'tuple'>
```

#### Tuple unpacking

```python
student = ("Marcy", 8, "History", 3.5)
# number of items in LHS must match RHS
name, age, subject, grade = student
name
'Marcy'
age
8
subject
'History'
grade
3.5

# let say there was a value we did not care about, use underscore
student = ("Marcy", 8, "History", 3.5)
name, age, subject, _ = student
```

### zip

In Python, the `zip` function is used to combine two or more iterables (such as lists, tuples, or arrays) into a single iterable of tuples.

>In this example, the `zip` function takes two lists as input and returns a list of tuples, where each tuple contains one element from each of the input lists.

```python
list1 = [1, 2, 3]
list2 = [10, 20, 30]

result = list(zip(list1, list2))

print(result)
# Output: [(1, 10), (2, 20), (3, 30)]
```

You can also use the `zip` function to unzip a list of tuples back into separate lists, using the following code:

>In this example, the `*` operator is used to unpack the list of tuples, and the `zip` function is used to combine the elements back into separate lists.

```python
zipped = [(1, 10), (2, 20), (3, 30)]

unzipped = list(zip(*zipped))

print(unzipped)
# Output: [(1, 2, 3), (10, 20, 30)]

```

### Sets
- A `set` is a **mutable datatype** that allows you to store **immutable** types in an **unsorted** way. 
	- They can contain *immutable* items, like `tuple`s and other primitive types
	- Cannot store mutable types like `list`s, `set`s, or `dict`ionaries
- Sets are mutable because you can add and remove items from them. 
- Cannot contain duplicate values

```python
# Various ways to create a set
set1={1,2,3,4,5,"hello","tup"}
set2={(1,8,"python",7)}
```

| type               | `set`                                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------------------- |
| use                | Used for storing immutable data types uniquely. Easy to compare the items in `set`s.                      |
| creation           | `set()` for an empty set (`{}` makes an empty `dict`) and `{1, 2, 3}` for a set with items in it          |
| search methods     | `item in my_set`                                                                                          |
| search speed       | Searching for an item in a large set is very fast.                                                        |
| common methods     | `my_set.add(item)`, `my_set.discard(item)` to remove the item if it's present, `my_set.update(other_set)` |
| order preserved?   | **No**. Items *can't* be accessed by index.                                                               |
| mutable?           | **Yes**. Can add to or remove from `set`s.                                                                |
| in-place sortable? | **No**, because items aren't ordered.                                                                     |

#### Empty Set

You can’t create an empty `set` with `{}`. That creates a `dict`. Create an empty set with `set()` instead.
```python
# Creating an empty set incorrectly
my_new_set = {}
type(my_new_set)
<class 'dict'>

# Correctly
my_set = set()
type(my_set)
<class 'set'>
```

#### Duplicate Values

`set`s can’t contain duplicate values
```python
numbers = {3, 3, 2, 2, 1}
numbers
{1, 2, 3}
```

`set`s can be used to de-duplicate the items in a list
- Tip: Use this to your advantage when you need to quickly deduplicate the items in a `list` _if you don’t care about order_. Pass the `list` into the `set` constructor.
```python
names = ['Nina', 'Max', 'Nina']
set(names)
{'Nina', 'Max'}
```

#### Mutability

`set`s can’t contain mutable types
- You can consider a set to behave a lot like a dictionary that only contains keys (and no values). 

If you’re not sure if a type or an object is hashable, you can call the built-in `hash()` function on it.
```python
>>> hash("Nina")
3509074130763756174
>>> hash([1, 2])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

#### Order

`set`s don’t have an order

Sets don’t have an order. That means that when you print them, the items won’t be displayed in the order they were entered in the list.
- It also means that you _can’t_ access items in the `set` by position in subscript `[]` notation.
```python
>>> my_set = {1, "a", 2, "b", "cat"}
>>> my_set
{1, 2, 'cat', 'a', 'b'}
```

#### Adding and removing from set

**Add items to a set with** `my_set.add(item)`.

```python
>>> colors = {"Red", "Green", "Blue"}
>>> colors.add("Orange")
>>> colors
{'Orange', 'Green', 'Blue', 'Red'}
```

**Remove items with** `my_set.discard(item)`

You can remove an item from a `set` if it’s present with `my_set.discard(item)`. If the set doesn’t contain the item, no error occurs.

```python
>>> colors = {"Red", "Green", "Blue"}
>>> colors.discard("Green")
>>> colors
{'Blue', 'Red'}
>>> colors.discard("Green")
>>> colors
{'Blue', 'Red'}
```

**Update a set with another sequence using** `my_set.update(sequence)`
You can add to the items in a `set` by passing in another sequence such as a `set`, `list`, or `tuple` to the `update()` method.

```python
>>> colors = {"Red", "Green"}
>>> numbers = {1, 3, 5}
>>> colors.update(numbers)
>>> colors
{1, 3, 'Red', 5, 'Green'}
```

#### Set operations
method operation | symbol operation | result |
| ---- | --------- | ----------- |
| `s.union(t)` | <code>s &#124; t</code> | creates a new `set` with all the items **from both `s` and `t`**|
| `s.intersection(t)`    |         `s & t`  |       creates a new `set` containing *only* items that are **both in `s` and in `t`**      |

```python
>>> rainbow_colors = {"Red", "Orange", "Yellow", "Green", "Blue", "Violet"}
>>> favorite_colors = {"Blue", "Pink", "Black"}

>>> rainbow_colors | favorite_colors
{'Orange', 'Red', 'Yellow', 'Green', 'Violet', 'Blue', 'Black', 'Pink'}

>>> rainbow_colors & favorite_colors
{'Blue'}
```

### Dictionaries

- Dictionaries are a useful type that allow us to store our data in key, value pairs. Dictionaries themselves are **mutable**, _but_, just like sets, dictionary keys can only be **immutable** types.
- dictionary values do not need to be mutable `my_numbers = {"one" : [1,2,3]`

```python
# Various way to create dictionaries
dict1={"key1":"value1","key2":"value2"}
dict2={} # empty dictionary
dict3=dict({1:"apple",2:"cherry",3:"strawberry"})
```

| type                      | `dict`                                                                                                                                                                                                                                                                                      |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| use                       | Use for storing data in key, value pairs. Keys used must be **immutable** data types.                                                                                                                                                                                                       |
| creation                  | `{}` or `dict()` for an empty `dict`. `{1: "one", 2: "two"}` for a `dict` with items.                                                                                                                                                                                                       |
| search methods            | `key in my_dict`                                                                                                                                                                                                                                                                            |
| search speed              | Searching for a key in a large dictionary is fast.                                                                                                                                                                                                                                          |
| common methods            | `my_dict[key]` to get the value by `key`, and throw a `KeyError` if `key` is not in the dictionary. Use `my_dict.get(key)` to fail silently if `key` is not in `my_dict`. `my_dict.items()` for all key, value pairs, `my_dict.keys()` for all keys, and `my_dict.values()` for all values. |
| order preserved?          | **Sort of**. As of Python 3.6 a `dict` is sorted by insertion order. Items *can't* be accessed by index, only by key.                                                                                                                                                                       |
| mutable?                  | **Yes**. You can add or remove keys from `dict`s.                                                                                                                                                                                                                                           |
| in-place sortable?        | **No**. `dict`s don't have an index, only keys.                                                                                                                                                                                                                                             |
| Accessing                 | ` my_dict[key]` *return error if no key* or `my_dict.get(key)` *no key returns None* or `my_dict.get(key, default_val)` *provides default value*                                                                                                                                            |
| Adding and Removing Items | `my_dict[key] = value` or `my_dict.update()` or my_dict.append                                                                                                                                                                                                                              |
| Accessing values          | `my_dict.keys()` - get all keys  `my_dict.values()` - get all values  `my_dict.items()` - get all items (key, value pairs)                                                                                                                                                                                                                                                                                    |

## Functions

The recipe for a function in Python:
1. `def`: the `def` keyword, telling Python we're about to start a function definition
1. a name for the function
1. `(`: opening parenthesis
1. (optional) the **names** of one or more arguments, separated with `,`
1. (optional) the **names** and **values** of one or more default arguments, separated with (`,`) *note: we'll see these in the next section*
1. `)` closing parenthesis
1. `:` a colon

```python
# A Basic Function that accepts no arguments and returns nothing.
def hello_world():
    print("Hello, World!")
# A Function that accepts two arguments, and returns a value
def add_numbers(x, y):
    return x + y
```

### Default Arguments

```python
# With Default Arguments
def say_greeting_with_default(name, greeting="Hello", punctuation="!"):
    print(f"{greeting}, {name}{punctuation}")
    
say_greeting_with_default("Nina")

say_greeting_with_default("Nina", "Good Day")
```

- Default arguments must be last
- don't use mutable types as default arguments
	- Instead create the list inside the function 

```python
def do_stuff(my_list=None):
	# Check if list is empty
	if my_list == None:
		my_list = [] # Create empty list
my_list.append("Stuff") # Append item to list
return my_list
```

## Boolean Logic

| type                                        	| truthiness                                                                     	|   	|
|---------------------------------------------	|--------------------------------------------------------------------------------	|---	|
| `int`                                       	| `0` is `False`, all other numbers are `True` (including negative)              	|   	|
| containers - `list`, `tuple`, `set`, `dict` 	| empty containers evaluate to `False`, containers with items evaluate to `True`) 	|   	|
| `None`                                      	| `False`                                                                        	|   	|


>Tip: If you want to test your assumptions about an expression that returns `True` or `False`, you can pass it into the constructor for `bool`eans: `bool(expression)`.


```python

>>> bool(0)
False
>>> bool(1)
True
>>> bool(-1)
True
```

### Equality Cheat Sheet

|Operator|Means|
|---|---|
|`==`|equals|
|`!=`|not-equals|

### Order Comparisons Cheat Sheet

|Operator|Means|
|---|---|
|`<`|less-than|
|`<=`|less-than-or-equal-to|
|`>`|greater-than|
|`>=`|greater-than-or-equal-to|

### Identity Cheat Sheet

|Operator|Means|
|---|---|
|`is`| *is* the same object in memory? (not equality!)|
|`is not`| *is not* the same object in memory? (not equality!)|

The `is` keywords tests if the two compared objects are stored in the same memory location. I won't go into too much detail into why, but remember **not** to use `is` when what you actually want to check for is equality.

>This is something that trips up Python beginners, so make sure you remember that *equality* (`==`, `!=`) **is not** the same as *identity* (`is`, `not is`).

>When you're first starting out, the only place you'll want to use the `is` keyword is to explicitly compare a value to the built-in types of `None`, `True`, or `False`.

```python
>>> a = True
>>> a is True
True

>>> b = False
>>> b is False
True
>>> b is not True   # Opposite of is b True. aka is b False?
True

>>> c = None
>>> c is None
True
>>> c is not None
False
```

### `and`, `or`, `not` Cheat Sheet

|Operation|Result|
|---|---|
|`a or b`|if a is `False`, then b, else a|
|`a and b`|if a is `False`, then a, else b|
|`not a`|if a is `False`, then `True`, else `False`|

| a       	| `not` a    	|
|---------	|------------	|
| `True`  	| `False`	|
| `False` 	| `True` 	|

##  if Statement and Conditionals

`if` in Python means: **only run the rest of this code once, *if* the condition evaluates to `True`.** 

```python
>>> if 3 < 5:
...     print("Hello, World!")
...
Hello, World!
```

If you only want your code to run if the expression is `False`, use the `not` keyword.

```python
>>> b = False
>>> if not b:
...     print("Negation in action!")
...
Negation in action!
```

`if` statements also work with items that have a "truthiness" to them.

```python
>>> message = "Hi there."

>>> a = 0
>>> if a:   # 0 is False-y
...     print(message)
...

>>> b = -1
>>> if b:  # -1 is Truth-y
...     print(message)
...
Hi there.

>>> c = []
>>> if c:  # Empty list is False-y
...     print(message)
...

>>> d = [1, 2, 3]
>>> if d:  # List with items is Truth-y
...     print(message)
...
Hi there.

>>> e = ""
>>> if e:
...     print(message)
...
```

You can easily declare `if` statements in your functions, you just need to mindful of the level of indentation.

```python
>>> def modify_name(name):
...    if len(name) < 5:
...         return name.upper()
...    else:
...         return name.lower()
...
>>> name = "Nina"
>>> modify_name(name)
'NINA'
```

### How *Not* To Use `if` Statements

```python
# Warning: Don't do this!
>>> if (3 < 5) == True: # Warning: Don't do this!
...     print("Hello")
...
Hello

# Warning: Don't do this!
>>> if (3 < 5) is True: # Warning: Don't do this!
...     print("Hello")
...
Hello

# Do this instead
>>> if 3 < 5:
...     print("Hello")
...
Hello
```

### else

The `else` statement is what you want to run **if and only if** your `if` statement wasn't triggered.

An `else` statement is part of an `if` statement. If your `if` statement ran, your `else` statement will never run.

```python
>>> a = True
>>> if a:
...     print("Hello")
... else:
...     print("Goodbye")
...
Hello
```

### elif

`elif` means *else if*. It means, **if** this `if` statement isn't considered `True`, try this **instead.**

>You can have as many `elif` statements in your code as you want. They get evaluated in the order that they're declared **until** Python finds one that's `True`. That runs the code defined in that `elif`, and skips the rest.

```python
>>> a = 5
>>> if a > 10:
...     print("Greater than 10")
... elif a < 10:
...     print("Less than 10")
... elif a < 20:
...     print("Less than 20")
... else:
...     print("Dunno")
...
Less than 10
```

## Loops

The syntax is: 1. `for single_item in items`

```python
>>> colors = ["Red", "Green", "Blue", "Orange"]
>>> for color in colors:
...     print(f"The color is: {color}")
...
The color is: Red
The color is: Green
The color is: Blue
The color is: Orange
```

### Looping over a range of numbers

```javascript
for (i = 0; i < 5; i++) {
  text += "The number is " + i + "<br>";
}
```

Writing the above javascript code in python

```python
>>> for num in range(5):
...     print(f"The number is: {num}")
...
The number is: 0
The number is: 1
The number is: 2
The number is: 3
The number is: 4
```

You'll notice that this call didn't *include* the number 5.

What if we wanted the range from 1 to 4, instead of 0 to 4? `range()` can be called with `start` and `stop` parameters, and the range will *start* from `start`.

```python
>>> for num in range(1, 5):
...     print(f"The number is: {num}")
...
The number is: 1
The number is: 2
The number is: 3
The number is: 4
```

You can also pass an a third optional `step` parameter in. 
`range(start, stop[, step])`

```python
>>> for num in range(2, 11, 2):
...     print(f"The number is: {num}")
...
The number is: 2
The number is: 4
The number is: 6
The number is: 8
The number is: 10
```

### Looping over items with the index using `enumerate`.

`enumerate(iterable, start=0)`

We need a way to access the index of the items we're looping through. To do that we use a special function called `enumerate()`. The function takes a sequence, like a `list`, and it *returns* a `list` of tuples, containing the index of the item in the sequence, and the sequence itself.

>Because `enumerate()` returns a structure that looks like a list of `tuple`s under the hood, we can take advantage of tuple unpacking in the `for` loop.

```python
>>> for index, item in enumerate(colors):
...     print(f"Item: {item} is at index: {index}.")
...
Item: Red is at index: 0.
Item: Green is at index: 1.
Item: Blue is at index: 2.
Item: Orange is at index: 3.
```

### Looping over a dictionary

Remember, a dictionary is composed of key, value pairs. When we loop over a dictionary with the `for item in my_dict` syntax, we'll end up looping over **just** the keys.

We can use tuple unpacking along with the `my_dict.items()` list to loop over both the keys and the values at the same time.

```python
>>> for color, hex_value in hex_colors.items():
...     print(f"For color {color}, the hex value is: {hex_value}")
...
For color Red, the hex value is: #FF0000
For color Green, the hex value is: #008000
For color Blue, the hex value is: #0000FF
```

#### Common Errors

What if you try to loop over key, value pairs, and forget to use `my_dict.items()`?

```python
>>> for color, hex_value in hex_colors:
...     print(f"For color {color}, the hex value is: {hex_value}")
...
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: too many values to unpack (expected 2)
```

>You'll see `ValueError: too many values to unpack (expected 2)` if you *forget* to call `my_dict.items()`, and try to loop over what you'd expect to be key, value pairs.

### While loops

```python
>>> counter = 0
>>> max_val = 4
>>>
>>> while counter < max_val:
...     print(f"The count is: {counter}")
...     counter = counter + 1
...
The count is: 0
The count is: 1
The count is: 2
The count is: 3
```


### Loops and the `return` statement

Just like in functions, consider the `return` statement the hard kill-switch of the loop.

```python
>>> def name_length(names):
...     for name in names:
...             print(name)
...             if name == "Nina":
...                     return "Found the special name"
...
>>> names = ["Max", "Nina", "Rose"]
>>> name_length(names)
Max
Nina
'Found the special name'
```

## Comprehensions

### List Comprehensions

A simple case: Say we want to turn a list of strings into a list of string _lengths._ We could do this with a `for` loop:

```python
>>> names = ["Nina", "Max", "Rose", "Jimmy"]
>>> my_list = [] # empty list
>>> for name in names:
...     my_list.append(len(name))
...
>>> print(my_list)
[4, 3, 4, 5]
```

```python
>>> names = ["Nina", "Max", "Rose", "Jimmy"]

>>> my_list = [len(name) for name in names]

>>> print(my_list)
[4, 3, 4, 5]
```

>List comprehensions will commonly take the form of `[<value> for <vars> in <iter>]`
>1. Start with empty list `[]`
>1. Type what I am looping over `[for name in names]`
>1. Type in what result I want `[len(name) for name in names]`

We can also use comprehensions to perform operations, and the lists we assemble can be composed of any type of Python object. For example:

```python
>>> names = ["Nina", "Max", "Rose", "Jimmy"]

>>> my_list = [("length", len(name) * 2) for name in names]

>>> print(my_list)
[('length', 8), ('length', 6), ('length', 8), ('length', 10)]
```

### Conditionals

You can also use conditionals (`if` statements) in your list comprehensions. For example, to quickly make a list of only the even lengths, you could do:

- if condition at the end

```python
>>> names = ["Nina", "Max", "Rose", "Jimmy"]

>>> my_list = [len(name) for name in names if len(name) % 2 == 0]

>>> print(my_list)
[4, 4]
```

### Split and Join

Strings have two functions for splitting and joining - `split()` and `join()`. 
- Calling `split()` on a string will split the string into a list, creating a new element for every instance of the character(s) you pass in. 
- `join()` accepts a list of strings, and uses the string you call it on to join the list together into one string. For example:

```python
>>> my_data = "this,is,comma,separated,data"
>>> my_data = my_data.split(",")
>>> print(my_data)
['this', 'is', 'comma', 'separated', 'data']

>>> ":".join(my_data)
'this:is:comma:separated:data'

>>> ", ".join(my_data)
'this, is, comma, separated, data'
```

### String Joining with a List Comprehension and Map

```Python
# List Comprehension with list joining
my_nums = [1, 2, 3]
join_num_list = ", ".join([str(num * 2) for num in my_nums])
print (join_num_list, type(join_num_list))
>>> 2, 4, 6 <class 'str'>

# Using Map
join_num_list_map = ", ".join(map(lambda num: str(num * 2), my_nums))
print(join_num_list_map, type(join_num_list_map))
>>> 2, 4, 6 <class 'str'>
```

>`map` and a list comprehension followed by `join` are two different ways to process elements in a list and produce a string representation of those elements.

`map` is a built-in Python function that applies a given function to each element of an iterable (e.g. a list) and returns a map object (an iterator) containing the results.

>In conclusion, both `map` and a list comprehension followed by `join` can be used to produce the same result, but list comprehensions tend to be more readable and concise.

### sum, min, max

Some mathematical functions, such as `sum`, `min`, and `max`, accept lists of numbers to operate on. For example, to get the sum of numbers between zero and five, you could do:

```python
>>> my_sum = sum([num for num in range(0, 100) if num % 3 == 0])
>>> print(my_sum)
1683
>>> my_min = min([num for num in range(0, 100) if num % 3 == 0])
>>> print(my_min)
0
>>> my_max = max([num for num in range(0, 100) if num % 3 == 0])
>>> print(my_max)
99
```

> Anywhere you can use a list, you can use a list comprehension.

### Dictionary Comprehensions

Dictionary comprehensions are a quick and easy way of assembling dictionaries in Python. 
- They work just like list comprehensions, and look almost the same. 
- They use curly braces instead of square brackets, and they contain two variables (for `key` and `value`), separated by a colon.

```python
>>> squares = {num:num * num for num in range(10)}

>>> print(squares)
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81}
```

We can even convert a list comprehension to a set then convert that to an object

```python
# We can even convert a list comprehension to a set then convert that to an object
my_list = [(f"player-{num}", num * 2) for num in range(0, 5)]
print(my_list, type(my_list))

# Convert set to object
scores = {key:value for (key, value) in my_list}
print(scores)
```

### Set Comprehensions

Set comprehensions are another great operation in Python - they look like a cross between `list` and `dict` comprehensions, and they create `set` objects.

```python
>>> my_set = {num for num in [1, 2, 1, 0, 3]}
>>> print(my_set)
{0, 1, 2, 3}
```

### Generator Expressions

A generator is a type of iterable object - like a list, you can iterate through each element - **however, unlike a list, generators evaluate elements on demand**, instead of assembling them all at once.

- A generator comprehension looks just like a list comprehension, except we use parentheses instead of brackets.

```python
# List comprehension
>>> list_comp = [x ** 2 for x in range(10) if x % 2 == 0]

>>> print(list_comp)
[0, 4, 16, 36, 64]

# Generator expression
>>> gen_exp = (x ** 2 for x in range(10) if x % 2 == 0)
>>> print(num)
...
0
4
16
36
64
```

Generator expressions offer improvements in memory use as execution speed, but are functionally different than lists.

Generators are **exhausted**, meaning you can only loop over them once, and you can't reference items in a generator without first converting it to a list.

If we try to loop over the generator created in the previous example a second time, we won't see any results.

Some common use cases for generators include:

-   Processing large files, where you only need to read a portion of the file at a time
-   Implementing lazy evaluation, where the next value is only generated when it is needed
-   Implementing infinite streams or sequences, such as a sequence of Fibonacci numbers
-   Implementing data pipelines, where the output of one generator can be used as the input to another generator.

Generators are also efficient, as they use a yield statement to return values one at a time, rather than building an entire list or array in memory.

## Slicing

`slice(start, stop[, step])`

```python
>>> my_string = "Hello, world!"
>>> my_string[7:12] # from 7 to 12
'world'
```

### Lopsided Slicing

You can also leave out one of the numbers in the slice. Leaving out the first number is equivalent to using a zero - you can think of this as *"from the beginning to"*

Leaving out the last number is equivalent to using the length of the list you're slicing - you can think of this as *"until the end."*

```python
>>> my_string = "Hello, world!"
>>> my_string[:5] # from zero to 5
'Hello'
>>> my_string[7:] # from 7 to the end
'world!'
```

You can also leave out both sides of the slice! You can think of this as *"from the beginning, until the end."* Why? *This is an easy way to copy a list!*

```python
>>> my_new_string = my_string[:]
>>> my_new_string
'Hello, world!'
```

### Negative Indexing

You aren't limited to positive numbers for your slicing, either. 
- A negative number on the left side will wrap around to the other side of your list.
- A negative number on the right side is equivalent to the length of the list minus your number. 

```python
>>> my_string = "Hello, world!"
>>> my_string[-6:] # from the end - 6 to the end
'world!'
>>> my_string[-10:-4] # from the end - 10 to the end - 4
'lo, wo'
```

You can also use just a single negative number to get an item counting _backwards_ from the end of a `list`. For example, to get the last item from a list:

```python
>>> my_list = [1, 3, 3, 7]
>>> my_list[-1]
7
```

### Stride or Step

Python slices also have a _third_, optional argument, called "step" or "stride", separated by a second colon. This lets you skip elements of a list or even reverse them. For example:

```python
>>> my_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> my_list[::2] # move forward by 2, or skip every other index
[0, 2, 4, 6, 8]
>>> my_list[::-1] # move backward by 1, and easy way to reverse a list
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
>>> my_list[1:7:2] # get every other index between 1 and 7
[1, 3, 5]
```

>You can use a slice to get a subset of items from any data type that maintains an order, such as a `list` or `tuple`, but not from any non-ordered data types, such as `dict` or `set`.

