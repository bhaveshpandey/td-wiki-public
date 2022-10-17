# asyncio

Async is not `multi-threading`.

Following is a very simple async event loop.


## asyncio.run

```python

import asyncio
import time


async def main():
    print(f"{time.ctime()} \t Starting!")
    await asyncio.sleep(1)
    print(f"{time.ctime()} \t Ending!")


asyncio.run(main())
```


## asyncio.run_in_executor

`Asyncio` also provides a functionality to offload a `compute-intensive` or a `cpu blocking` task to another thread. This allows asyncio to continue working within its own thread.

```python

import asyncio
import time

from faker import Faker

# Example showing how to execute a blocking/compute intensive task on a different
# thread than asyncio.


async def main():
    f = Faker()
    for i in range(10):
        print(f"{time.ctime()}\t MESSAGE:  {f.text(30)}")
        await asyncio.sleep(1)


async def wrap_to_run_in_exec(fn, value):
    lp = asyncio.get_event_loop()
    await lp.run_in_executor(None, fn, value)


# The following routine is a blocking routine using time.sleep which doesn't yield back
# the control. Running this in another thread, allows us to offload some long running
# computation to another thread while still using asyncio.
def blocking(nsec):
    for i in range(10):
        s = time.time()
        print(f"{time.ctime()}\t EXECUTOR THREAD :  Starting a blocking routine")
        time.sleep(nsec)
        print(
            f"{time.ctime()}\t EXECUTOR THREAD :ELAPSED:  {time.time()-s}\t  for an Iteration."
        )


async def parallel():
    await asyncio.gather(main(), wrap_to_run_in_exec(blocking, 1))

asyncio.run(parallel())
```


## AIOHTTP

Following is an example async web server.

```python

import asyncio as aio

from aiohttp import web


async def echo_handler(request):
    response = web.Response(text=request.match_info["what"])
    await response.prepare(request)
    return response


async def start_server(runner):
    await runner.setup()
    site = web.TCPSite(runner, "localhost", 8080)
    await site.start()


if __name__ == "__main__":
    app = web.Application()
    app.router.add_route("GET", "/echo/{what}", echo_handler)

    runner = web.AppRunner(app=app)
    loop = aio.get_event_loop()
    loop.create_task(start_server(runner))
    loop.run_forever()
    loop.close()
```



## Resources

* [Lynn Root - Advanced asyncio: Solving Real-world Production Problems - PyCon 2019](https://www.youtube.com/watch?v=bckD_GK80oY&t=430s)
* [David Beazely - The Other Async (Threads + Async)](https://www.youtube.com/watch?v=x1ndXuw7S0s)
* [David Beazely Fear and Awaiting in Async](https://www.youtube.com/watch?v=E-1Y4kSsAFc)

* [Python Async Basics - 100 Millions http requests](https://www.youtube.com/watch?v=Mj-Pyg4gsPs)
* [Miguel Grinberg - asyncio for complete beginner](https://www.youtube.com/watch?v=iG6fr81xHKA)


### Resources from Raymond Hettinger

* [Raymond Hettinger, Keynote on Concurrency, PyBay 2017](https://www.youtube.com/watch?v=9zinZmE3Ogk&t=679s)
