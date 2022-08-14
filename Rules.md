**Docstrings and annotations**

Explain what it is supposed to do (not how). With the autodoc extension (sphinx.ext.autodoc) we can take the docstrings from the code and place them in the pages that document the function. 

The basic idea of annotations is to hint to the readers of the code about what to expect as values of arguments in functions. It is actually not only about the types, but any kind of metadata that can help you get a better idea of what that variable actually represents.

`class Point:
 def __init__(self, lat, long):
 self.lat = lat
 self.long = long
def locate(latitude: float, longitude: float) -> Point:
"""Find an object in the map by its coordinates"""`




