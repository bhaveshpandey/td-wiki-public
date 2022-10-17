# Operators

## Documentation

Following are some really good resources for the documentation. Refer to the marble diagrams for a better understanding of the operators.

* [ReactiveX](https://reactivex.io/documentation/operators.html)
* [Operator Marble Diagrams](https://rxmarbles.com/#zip)


## Core Operators


### zip

Combines 2 or more observables into a single stream/observable which only emits if all the component streams have a latest value.

```python

import reactivex as rx
from reactivex import operators as ops
import datetime

stream1 = rx.interval(period=datetime.timedelta(seconds=2))
stream2 = rx.interval(period=datetime.timedelta(seconds=5))

both_streams = rx.zip(stream1, stream2)

both_streams.subscribe(
                        on_next=lambda i: print(f"event:  {i}"),
                        on_error=lambda e: print(f"error:  {e}")
                    )
```

The `Zip` operator will make the two streams depend on each other.


### group_by


### scan


### map


### flat_map

FlatMap also doubles up as a concurrent processing tool since all the observables processed by it will be done in parallel (subject to availability of CPU resources).


### switch_map

SwitchMap is very similar to `flat_map`. It is a really great operator for killing any previous tasks and starting new ones. This is ideal for Database queries based on user input (which can be debounced).
`SwitchMap` will kill any of the processes/tasks which are running as soon as new emissions become available and start new tasks.


### distinct


### distinct_until_changed


### filter


### start_with


### catch

An operator for catching `exceptions` within the pipeline and handling them.


### retry

Another operator related to errors during the execution of the pipelines. This operator will retry the erroring `upstream` operator said number of times.
If no retry value is specified, it will retry the operation `indefinitely` and `always`.

```python

ops.retry(4) # Retry 4 times before throwing an error

ops.retry()  # Keep retrying indefinitely
```
