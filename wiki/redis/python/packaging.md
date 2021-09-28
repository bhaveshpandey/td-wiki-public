# Packaging

:python:

## Using setuptools

```python
from setuptools import setup

setup(
    name="helloworld",  #name of the package which will be registered with PyPI
    version="0.0.1",
    description="blah",
    py_modules=["foo"],
    package_dir={"": "src"},
)

```

## Local installation

```python

# Following statement will install the package locally.
pip install -e .

# Following statement will install the package locally along with the "dev" package.
pip install -e .[dev]
```


## Resources

* [Publishing (Perfect) Python Packages on PyPi](https://www.youtube.com/watch?v=GIF3LaRqgXo&t=1473s)
* [How to Publish an Open-Source Python Package to PyPI](https://realpython.com/pypi-publish-python-package/)
* [Packaging a python library](https://blog.ionelmc.ro/2014/05/25/python-packaging/)
