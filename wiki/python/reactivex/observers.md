# Observers

## Custom Observers

We can subclass the `Observable` class to create our own observables. Its important to definie the 3 methods on this class to make the subclass behave correctly.
1. `on_next`
2. `on_error`
3. `on_completed`

Following is a simplified example for the same.

```python

import logging

import reactivex as rx
from reactivex import operators as ops

from baselogger import logger

logger.setLevel(logging.DEBUG)


class CustomObserver(rx.Observer):
    def on_next(self, value):
        logger.info(f"on_next:  {value}")
        return value

    def on_error(self, error):
        logger.error(f"on_error:  {error}")

    def on_completed(self):
        logger.error("on_completed")


if __name__ == "__main__":
    stream = rx.from_iterable(range(4))

    observer = CustomObserver()
    stream.subscribe(observer)
```


Another way to creating a simple observable is to use a function instead of a class.

```python

import reactivex as rx
from reactivex import operators as ops

# NOTE:
# The following is simply a factory for our custom Observable.
# This is then used by the reactivex.create Factory method to instantiate
# and then hook up various functions correctly.
def custom_obs(observable, scheduler):
    observable.on_next("Next on my custom Observable, lets log to debug logger?")
    observable.on_error("Lets log errors to the logger?")
    observable.on_completed()


if __name__ == "__main__":
    # Create an instance of our observable
    data_stream = rx.create(custom_obs)
    data_stream.subscribe(
        on_next=lambda i: print(f"item:  {i}"),
        on_error=lambda e: print(f"error:  {e}"),
        on_completed=lambda: print(f"Completed.")
    )

```
