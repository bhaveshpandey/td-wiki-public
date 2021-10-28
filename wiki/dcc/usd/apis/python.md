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
stg.DefinePrim("/world")
stg.Save()
```

## Asset Resolution
Asset Resolution is responsible for resolving relative paths defined in USD assets to absolute paths.

```python
from pxr import Ar

Ar.SetDefaultSearchPath(["/home/atoi/dev/assets/foo",])
resolver = Ar.GetDefaultResolver()
path = resolver.Resolve("comp/task.usda")
```


## Traversing References within a stage
```python
from pxr import Usd

# Lets open some USD stage with references
stg = Usd.Stage.Open("/path/to/usd/file.usda")
refs = stg.GetRootLayer().GetExternalReferences()
```
