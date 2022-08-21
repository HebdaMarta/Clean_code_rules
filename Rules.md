# Docstrings and annotations

Explain what it is supposed to do (not how). With the autodoc extension (sphinx.ext.autodoc) we can take the docstrings from the code and place them in the pages that document the function. 

The basic idea of annotations is to hint to the readers of the code about what to expect as values of arguments in functions. It is actually not only about the types, but any kind of metadata that can help you get a better idea of what that variable actually represents.

```
class Point:
   def __init__(self, lat, long):
    self.lat = lat
    self.long = long
   def locate(latitude: float, longitude: float) -> Point:
   """Find an object in the map by its coordinates"""
```

[**Mypy**](https://mypy-lang.org) is the main tool for optional static type checking in Python. **Pylint** is tool for checking the structure of the code (compliance with PEP-8). **Makefiles** are  tools that let us configure commands to be run in the project, mostly for compiling, running, and so on. Besides this, we can use a makefile in the root of our project, with some commands configured to run checks of the formatting and conventions on the code, automatically.

You should:
1. First check the compliance with the coding guideline (PEP-8, for instance).
2. Then check for the use of types on the code.
3. Finally, run the tests.

Besides it is also a good idea adopts a convention and an automatic approach for structuring the code. Tools such as [**Black**](https://github.com/ambv/black) automatically format the code.

# Pythonic Code

**Context manager**

Context managers consist of two magic methods: __enter__ and __exit__. 

---

The **with** statement enters the context manager. In this case, the open function implements the context manager protocol, which means that the file will be automatically closed when the block is finished, even if an exception occurred. On the first line of the context manager, the with statement will call the first method, __enter__, and whatever this method returns will be assigned to the variable labeled after as. This is optional - we don't really need to return anything specific on the __enter__ method, and even if we do, there is still no strict reason to assign it to a variable if it is not required.

---

The *contextlib* module contains a lot of helper functions and objects to either implement context managers or use some already provided ones. 

**Underscores: _**

All of the properties and functions of an object are public in Python. Objects should only expose those attributes and methods that are relevant to an external object. Everything that is not strictly part of an object's interface should be kept prefixed with a single underscore. This is the Pythonic way of clearly delimiting the interface of an object.

The idea of the double underscore in Python means to override different methods of a class that is going to be extended several times, without the risk of having collisions with the method names. Double underscores are not a Python approach (don't use them) - to define attributes as private, use a single underscore and follow the Python convention that it's a private attribute.

**Properties: _@property_**

Properties are to be used when we need to define access control to some attributes in an object. In other programming languages (like Java), you would create access methods (getters and setters).

```
import re

EMAIL_FORMAT = re.compile(r"[^@]+@[^@]+\.[^@]+")

def is_valid_email(potentially_valid_email: str):
 return re.match(EMAIL_FORMAT, potentially_valid_email) is not None
 
class User:
  def __init__(self, username):
   self.username = username
   self._email = None
   
  @property
  def email(self):
   return self._email
   
  @email.setter
  def email(self, new_email):
   if not is_valid_email(new_email):
    raise ValueError(f"Can't set {new_email} as it's not a valid email")
   self._email = new_email
```
The *@property* decorator is the query that will answer to something, and the *@<property_name>.setter* is the command that will do something.

---
Methods should do one thing only.

---

**Iterable objects**

In Python, we have objects that can be iterated by default (f.e lists, tuples, sets, and dictionaries), but we could also create our own iterable, with the logic we define for iteration. When we try to iterate an object, Python will call the `iter()` function over it.

**Container objects**

Containers are objects that implement a `__contains__` method (that usually returns a Boolean value). This method is called in the presence of the `in` keyword of Python (f.e. `element in container` = `container.__contains__(element)`).

**Dynamic attributes for objects**

It is possible to control the way attributes are obtained from objects by means of the `__getattr__` magic method. When we call something like _myobject_._myattribute_ , Python will look for _myattribute_ in the dictionary of the object, calling `__getattribute__` on it. If this is not found (namely, the object does not have the attribute we are looking for), then the extra method, `__getattr__`, is called, passing the name of the attribute (myattribute) as a parameter. By receiving this value, we can control the way things should be returned to our objects. We can even create new attributes, and so on.
 
 ```
 class DynamicAttributes:
  def __init__(self, attribute):
   self.attribute = attribute
 
  def __getattr__(self, attr):
   if attr.startswith("fallback_"):
    name = attr.replace("fallback_", "")
    return f"[fallback resolved] {name}"
   raise AttributeError(f"{self.__class__.__name__} has no attribute {attr}")
 
 ```
 **Callable objects**
 
It is possible to define objects that can act as functions. One of the most common applications for this is to create better decorators, but it's not limited to that.
The magic method `__call__` will be called when we try to execute our object as if it were a regular function. The main advantage of implementing functions this way, through objects, is that objects have states, so we can save and maintain information across calls. When we have an object, a statement like this `object(*args, **kwargs)` is translated in Python to `object.__call__(*args, **kwargs)`. 
 
 ```
 from collections import defaultdict

 class CallCount:
 
  def __init__(self):
   self._counts = defaultdict(int)
   
  def __call__(self, argument):
   self._counts[argument] += 1
   return self._counts[argument]
 ```
 
 **Summary**
 
 ![image](https://user-images.githubusercontent.com/71260762/185752201-02f9014f-0807-4248-ae82-dbf68cbb0609.png)

**Caveats**

1. Don't use mutable objects as the default arguments of functions
2. Don't extend directly from dict, use `collections.UserDict` instead. For lists, use `collections.UserList`, and for strings, use `collections.UserString`. The correct way of extending built-in types such as lists, strings, and dictionaries is by means of the collections module.

# General Traits of Good Code








 

