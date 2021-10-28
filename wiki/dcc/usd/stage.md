# Stage

A **Stage** in USD refers to a final scene graph configuration which comprises of other layers.

Given a stage **stg** with UsdPrim **foo**, **foo's** children within the stage can be queried using

```python

foo = stg.GetPrimAtPath("/foo")
foo.GetAllChildren()
```
