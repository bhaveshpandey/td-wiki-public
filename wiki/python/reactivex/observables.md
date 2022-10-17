# Observables/Streams

An entity which emits `items`.


## Cold Observables

Cold observables `ONLY` emit when an observable subscribes to it.


## Hot Observables

Hot observables mimic real-time events which can not be replayed and if an `Observer` subscribes to it after it has already started emitting, the `Observer` will miss the data.


## Custom Observables

Following is one of the ways we can create a custom `Observable`.

```python

import
```
