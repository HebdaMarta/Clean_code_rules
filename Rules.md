# Docstrings and annotations

Explain what it is supposed to do (not how). With the autodoc extension (sphinx.ext.autodoc) we can take the docstrings from the code and place them in the pages that document the function. 

The basic idea of annotations is to hint to the readers of the code about what to expect as values of arguments in functions. It is actually not only about the types, but any kind of metadata that can help you get a better idea of what that variable actually represents.

`class Point:
 def __init__(self, lat, long):
 self.lat = lat
 self.long = long
def locate(latitude: float, longitude: float) -> Point:
"""Find an object in the map by its coordinates"""`

**Mypy** (http://mypy-lang.org/) is the main tool for optional static type checking in Python. **Pylint** is tool for checking the structure of the code (compliance with PEP-8). **Makefiles** are  tools that let us configure commands to be run in the project, mostly for compiling, running, and so on. Besides this, we can use a makefile in the root of our project, with some commands configured to run checks of the formatting and conventions on the code, automatically.

You should:
1. First check the compliance with the coding guideline (PEP-8, for instance).
2. Then check for the use of types on the code.
3. Finally, run the tests.

Besides it is also a good idea adopts a convention and an automatic approach for structuring the code. Tools such as **Black** (https://github.com/ambv/black) automatically format the code.

# Pythonic Code

**Context manager**

Context managers consist of two magic methods: __enter__ and __exit__. 

!The **with** statement enters the context manager. In this case, the open function implements the context manager protocol, which means that the file will be automatically closed when the block is finished, even if an exception occurred. On the first line of the context manager, the with statement will call the first method, __enter__, and whatever this method returns will be assigned to the variable labeled after as. This is optional—we don't really need to return anything specific on the __enter__ method, and even if we do, there is still no strict reason to assign it to a variable if it is not required.!




