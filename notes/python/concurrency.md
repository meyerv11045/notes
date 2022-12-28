# Concurrency

multithreading for network bound work

–	no benefit to in CPU intensive processing since its mostly for handling wait times in IO ops efficiently

–	GIL- only 1 thread can run python interpret at a time

–	multiprocessing for cpu bound work

–	what we are using

–	allows you to create programs that run concurrently, bypassing the GIL 

–	each process has its own interpreter and own GIL 

multiprocessing:

–	criteria for code that can be multiprocessed:

–	1) must not reliant on previous outcomes

–	2) Does not need to be executed in a paritcular order

–	3) Does not return anything that would need to be accessed later in the code

## Threading

- Daemon Threads- background threads that do not prevent program from exiting once there are no non-daemon threads remaining
  - A thread defaults to its parent process's status of being a daemon thread which for the main thread is false
- If you `.join()` a thread (daemonic or non-daemonic), the statement will wait until the thread is finished


## Multiprocessing

## Asyncio

- write concurrent code using `async`/`await` syntax
- good for IO-bound code
- high-level api is able to 
  - concurrently run/control python coroutinues/functions
  - work with IO streams
  - control subprocesses
  - distribute tasks via queues
  - synchronize concurrent code
- debug by passing `debug=True` to [`asyncio.run()`](https://docs.python.org/3/library/asyncio-task.html#asyncio.run).

### Coroutines

``` python
import asyncio

async def main():
	print('hello')
	await asyncio.sleep(1)
	print('world')

asyncio.run(main())
```

- calling `main()` does not execute the coroutine since it is a coroutine object
- can run a coroutine in 3 ways:
  1. `asyncio.run(coroutine())`
  2. `await coroutine()`
  3. `asyncio.create_task(coroutine())` and then `await` the task
- 3 types of awaitable objects: coroutines, tasks, and futures
- `asyncio.wait_for(awaitable, timeout)` raises a `asyncio.TimeoutError` 

