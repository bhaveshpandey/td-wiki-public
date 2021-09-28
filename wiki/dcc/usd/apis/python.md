# Python

USD's python API is simply a boost python wrapper around their C++ API. For all intents and purposes, view the USD C++ documentation to get insights on their python API.

## Imports
```python
from pxr import Usd
from pxr import Sdf
```

## Creating a Stage
```python
stg = pxr.Usd.Stage.CreateNew("foo.usda")
stg.Save()
```
