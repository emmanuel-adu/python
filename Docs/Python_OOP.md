## Table of Content

- [Object Oriented Programming](#Object-Oriented-Programming)
- [Classes](#Classes)
- [Methods](#Methods)
- [Inheritance](#Inheritance)

## Object Oriented Programming

In Python, everything is an object. An object is an instance of a class, which is a blueprint for creating objects.
- An object can be a function, a variable, a property, a class…

**Here are the key concepts of OOP in Python:**

1.  Class: A class is a blueprint for creating objects. A class definition usually starts with the `class` keyword, followed by the name of the class.
    
2.  Object: An object is an instance of a class. Objects have attributes, which are data stored inside the object, and methods, which are functions that operate on the object's data.
    
3.  Attribute: An attribute is a property of an object, which describes the state of the object.
    
4.  Method: A method is a function that operates on the object's data.
    
5.  Inheritance: Inheritance is a mechanism that allows you to create a new class that is a modified version of an existing class. The new class is called a subclass and the existing class is the superclass.
    
6.  Polymorphism: Polymorphism is the ability of objects of different classes to respond to the same method call in different ways.
    
7.  Encapsulation: Encapsulation is the idea of wrapping data and functions that work on that data within one unit, or object.

## Classes

Every thing or object in Python is an instance of a _class_. The number `42` is an instance of the class `int`. The string `Hello, world` is an instance of the `str` (or string) class. These classes, in turn, are subclasses of the master `object` class.

- `self` refers to an instance

```python
# Create Dog Class
class Dog:

	# Class Method, self must always be first arg
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

    def bark(self):
        print("Woof!")

# Create Dog Object 
dog = Dog("Fido", "Labrador")
dog.bark() # Output: Woof!

```

## Methods

### classmethods

`classmethod()` methods are bound to a class rather than an object. Class methods can be called by both class and object. These methods can be called with a class or with an object.

- class (`cls`) gets passed in instead of `self`

```python
class Car:
	runs = True
	number_of_wheels = 4

	@classmethod
	def get_number_of_wheels(cls): 
		return cls.number_of_wheels

	def start(self):
		if self.runs:
			print("Car is started. Vroom vroom!")
		else:
			print("Car is broken :(")
			
my_car = Car()
print(f"Cars have {Car.get_number_of_wheels()} wheels.")

# Of course, we can override this in our instance:
my_car.number_of_wheels = 6
# And when we access our new instance variable:
print(f"My car has {my_car.number_of_wheels} wheels.")
# But, when we call our class method on our instance:
print(f"My car has {my_car.get_number_of_wheels()} wheels.")
# Call class method with class:
print(Car.get_number_of_wheels())
```

### type, isInstance, issubclass

Python comes with some built-in functions for inspecting classes and types:

As we’ve seen throughout the workshop, the `type()` function returns the type of the object you pass it, or it’s class. For example:

```python
>>> type(42)
<class 'int'>
>>> type("Hello world!")
<class 'str'>
>>> type(my_car)
<class '__main__.Car'>
```

The `isinstance()` function takes an object and a class, and returns `True` if the object you pass it is an instance of the class. For example:

```python
>>> isinstance(42, int) 
True 
>>> isinstance("Hello world!", str) 
True 
>>> isinstance(my_car, float) 
False 
>>> isinstance(my_car, Car) 
True
```

The `issubclass` function takes two classes, and returns `True` if the first class is a subclass of the second. For example:

```python
# bool is a subclass of int
>>> issubclass(bool, int)
True
# int is a subclass of object
>>> issubclass(int, object)
True
# technically, everything is a subclass of object
>>> issubclass(bool, object)
True
```

### `__init__`

Classes can have an optional magic method called `__init__()` that gets run when you instantiate an instance of a class.

`__init__` method in Python is similar to a constructor in other programming languages. It's called automatically when an object of the class is created, and it's used to initialize the attributes of the object.

```python
class Car:
    runs = True
    
	# init 
    def __init__(self, make, model):
        self.make = make
        self.model = model

    def start(self):
        if self.runs:
            print(f"Your {self.make} {self.model} is started. Vroom vroom!")
        else:
            print(f"Your {self.make} {self.model} is broken :(")

my_car = Car("Ford", "Thunderbird")
my_car.start()
```

```zsh
Your Ford Thunderbird is started. Vroom vroom!
```

### `__str__` and `__repr__`

The `__str__` and `__repr__` methods in Python are used to represent the string representation of an object.

- `__str__()` should return readable end-user output
	- maps to the built-in function `str()`
- `__repr__()` should return the Python code necessary to rebuild the object
	- `__repr__()` maps to the built-in function `repr()`

For example, we’ll use the `datetime` library to generate a `datetime` object for right now:

```python
>>> import datetime
>>> now = datetime.datetime.now()
>>> str(now)
'2019-03-16 21:04:01.396256'
>>> repr(now)
'datetime.datetime(2019, 3, 16, 21, 4, 1, 396256)'
```

We can, of course, set our own `__str__()` and `__repr__()` methods in our custom classes:

```python
[](<class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name} is {self.age} years old."

    def __repr__(self):
        return f"Person({self.name!r}, {self.age!r})"

john = Person("John Doe", 30)
print(john.name)  # Output: John Doe is 30 years old.
print(str(john))  # Output: John Doe is 30 years old.
print(repr(john))  # Output: Person('John Doe', 30)>)
   
   ```

## Inheritance

Class inheritance is a very useful Object-oriented Programming construct for sharing and reusing code. 

- Inheritance makes it possible to break up and organize your code into a hierarchy, from generic to specific.
- Objects that belong to classes that are higher up in the hierarchy (more generic) are accessible by subclasses, but not vice versa.

We can do the same with our own classes, too. In a file called `vehicle.py`, let’s create a parent `Vehicle` class, and have our `Car` class be a subclass.

```python
# vehicle.py

class Vehicle:

    def __init__(self, make, model, fuel="gas"):
        self.make = make
        self.model = model
        self.fuel = fuel


class Car(Vehicle):

    def __init__(self, make, model, fuel="gas"):
        super().__init__(make, model, fuel)
```

```python
# chapter_6.py

from vehicle import Vehicle, Car

my_car = Car("Ford", "Thunderbird")
print(f"my_car is type {type(my_car)}")
print(f"my_car uses {my_car.fuel}")

print(f"my_car is a Car: {isinstance(my_car, Car)}")
print(f"my_car is a Vehicle: {isinstance(my_car, Vehicle)}")
print(f"Car is a subclass of Vehicle: {issubclass(Car, Vehicle)}")
```

```bash
(env) $ python chapter_6.py
my_car is type <class 'vehicle.Car'>
my_car uses gas
my_car is a Car: True
my_car is a Vehicle: True
Car is a subclass of Vehicle: True
```

### Overriding Variables in a Subclass

We can, of course, use a subclass to override variables that belong to a parent class. Let’s update our `vehicle.py` file:

```python
# vehicle.py

class Vehicle:
    number_of_wheels = 4

    def __init__(self, make, model, fuel="gas"):
        self.make = make
        self.model = model
        self.fuel = fuel

class Car(Vehicle):

    def __init__(self, make, model, fuel="gas"):
        super().__init__(make, model, fuel)

class Truck(Vehicle):
    number_of_wheels = 6

    def __init__(self, make, model, fuel="diesel"):
        super().__init__(make, model, fuel)

class Motorcycle(Vehicle):
    number_of_wheels = 2
```

```python
# chapter_6.py

from vehicle import Truck, Motorcycle
 
my_truck = Truck("Ford", "F350")
print(f"my_truck is type {type(my_truck)}")
print(f"my_truck uses {my_truck.fuel}")
print(f"my_truck has {my_truck.number_of_wheels} wheels")

my_motorcycle = Motorcycle("BMW", "Adventure")
print(f"my_motorcycle is type {type(my_motorcycle)}")
print(f"my_motorcycle uses {my_motorcycle.fuel}")
print(f"my_motorcycle has {my_motorcycle.number_of_wheels} wheels")
```

```bash
my_truck is type <class 'vehicle.Truck'>
my_truck uses diesel
my_truck has 6 wheels
my_motorcycle is type <class 'vehicle.Motorcycle'>
my_motorcycle uses gas
my_motorcycle has 2 wheels
```




