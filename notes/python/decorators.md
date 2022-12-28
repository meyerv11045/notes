# Decorators

## Basic

``` python
from functools import wraps

def stopwatch(f):
  @wraps(f) # preserves info from original function such as docstring
  def func(*args, **kwargs):
    start = time.time()
    res = f(*args, **kwargs)
    print(f"function took : {time.time() - start} seconds")
    return res

@stopwatch
def sleep_random(s=1):
  """Sleeps for random amount of time"""
  time.sleep(s + random.random()/100)
  return "DONE!"

sleep_random(2)

## above is equivalent to 
timed_func = stopwatch(sleep_random)
timed_func(2)
```

- using a decorator results in less repeat code: 1 function instead of 2
    - also more flexible for adding the functionality to other functions
- make sure to use `@wraps` when creating a decorator to avoid unintended side effects
- decorators stack and are executed from top to bottom order 
    - so if order of decorators matters, keep that in mind (but good decorators ideally don't rely on ordering)

## Parameterized

```python
from functools import wraps

def log(show_name=True, show_time=True):
  def stopwatch(f):
    @wraps(f)
    def func(*args, **kwargs):
      start = time.time()
      res = f(*args, **kwargs)
     	log_txt = "Call"
      if show_name:
        log_txt = f"{log_text} {f.__name__}"
      if show_time:
        log_txt = f"{log_text} time:{time.time() - tic}"
      print(log_txt)
      return res
    return func
  return stopwatch 

@log(show_name=False, show_time=True)
def sleep_random(s):
  """Function sleeps for at least s seconds"""
	time.sleep(s + random.random()/100)
  
# for default behavior
@log()
def sleep_random(s):
  """Function sleeps for at least s seconds"""
	time.sleep(s + random.random()/100)
```

- parameterized decorators give very customizable behavior
- (need the parentheses b/c it calls log() to return the stopwatch decorator)
- `def f(param1, * ,param2, param3)` the star makes all the params after it need to be passed via keyword args
- can make `@log` and `@log()` both work for default behavior:

``` python
def log(func_in=None, *, show_name=True, show_time=True):
    def stopwatch(f):
        @wraps(f)
        def func(*args, **kwargs):
            tic = time.time()
            result = f(*args, **kwargs)
            result = "call"
            if show_name:
                result = f"{result} {f.__name__}"
            if show_time:
                result = f"{result} time:{time.time() - tic}"
            return result
        return func
      
    # This is where the "magic" happens.
    if func_in is None:
        return stopwatch
    else:
        return stopwatch(func_in)

@log
def sleep_random(s):
    """This function sleeps at least for `s` seconds."""
    return time.sleep(s + random.random()/100)
```

## Applications

- Logging steps in a pandas pipeline
- `@retry(ValueError, tries=5, delay=0.1)` for retrying a function (useful when getting stuff from internet)
    - `from retry import retry`
- [Clumper reading dataset from multiple files](https://github.com/koaning/clumper/blob/main/clumper/decorators.py#L65)
- Least recently used cache: `@lru_cache(1000)` where the parm is the size of the cache
    - `from functools import lru_cache`
    - improves performance of recursive functions that have overlapping subproblems