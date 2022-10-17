# Packaging


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
pip install -e ."[dev]"
```


## Uploading to PyPI Python Packaging Index

Building the package

```sh

python setup.py sdist bdist_wheel
```

```python

python -m twine upload dist/*
```


## Inspect hash of a package

We can easily inspect the hash of a package available in PyPI index as follows.

```sh

# The following command will download the tarball or wheel which is available for the project in PyPI
python -m pip download legos-base

# We can then hash the tarball or the wheel as follows
python -m pip hash ./legos_base-0.0.1-py3-none-any.whl

# Output of above command is as follows**
./legos_base-0.0.1-py3-none-any.whl:
--hash=sha256:dc1be30fa5a4c035708002e80fa42528639ec0c059afddb3727d440b4a34a0c2
```


## Resources

* [Publishing (Perfect) Python Packages on PyPi](https://www.youtube.com/watch?v=GIF3LaRqgXo&t=1473s)
* [How to Publish an Open-Source Python Package to PyPI](https://realpython.com/pypi-publish-python-package/)
* [Packaging a python library](https://blog.ionelmc.ro/2014/05/25/python-packaging/)
