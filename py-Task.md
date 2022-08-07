# Python Task Management


###### _Table of Contents_

- Command Line Arguments
- Time
	1. Timestamp
	2. Datetime
	3. Timedelta
	4. Datetime String
- Multithreading
	1. Threads
	2. Timers
	3. Locks
	4. Reentrant Locks
	5. Condition Variables
	6. Semaphores
	7. Context Managers
- Launching Programs


## Command Line Arguments

When running a Python script from the command line, additional arguments can be specified.

[`sys.argv`](https://docs.python.org/3/library/sys.html#sys.argv) is the list of command line arguments passed to a Python script.
Usually `sys.argv[0]` is the script name passed to the interpreter.


## Time

### Timestamp

The **`time` module** offers time-related functions.

**System clock**

- `time.time()` returns the number of seconds since Unix epoch (12 AM UTC on 1 Jan 1970) as a float, which is called a Unix timestamp.
- `time.ctime(timestamp=None)` returns a string describes the time expressed in seconds since the epoch. Use current time if not provided.

**Pause program execution**

`time.sleep(seconds)` suspends execution of the calling thread for the given number of seconds.


### Datetime

A `datetime` object in the **`datetime` module** represents a specific moment in time.

**Initialization**

- `datetime.datetime(year, month, day, hour=0, minute=0, second=0, microsecond=0)` instantiates a `datetime` object.
- `datetime.datetime.now()` returns a `datetime` object for the current date and time, according to the computer clock.
- `datetime.datetime.fromtimestamp(timestamp)` converts an Unix epoch timestamp to a `datetime` object.

**Attributes**

1. `MINYEAR` <= `year` <= `MAXYEAR`
2. 1 <= `month` <= 12
3. 1 <= `day` <= number of days in the given month and year
4. 0 <= `hour` < 24
5. 0 <= `minute` < 60
6. 0 <= `second` < 60
7. 0 <= `microsecond` < 1000000

**Comparison**

`datetime` objects can be compared with each other using comparison operators. The later `datetime` object is the greater value.

### Timedelta

A `timedelta` object in the **`datetime` module** represents a duration of time.

**Initialization**

`datetime.timedelta(days=0, seconds=0, microseconds=0)` instantiates a `timedelta` object.

**Attributes**

1. -999999999 <= `days` <= 999999999
2. 0 <= `seconds` < 86400
3. 0 <= `microseconds` < 1000000

**Comparison**

- `timedelta` objects can be compared with each other using comparison operators.
- Instance method `td.total_seconds()` returns the total number of seconds contained in the duration as a float.

**Arithmetic**

1. A `timedelta` objects can be added or subtracted with `datetime` objects or other `timedelta` objects using the `+` and `-` operators.
2. A `timedelta` object can be multiplied or divided by integer or float values with the `*` and `/` operators.

### Datetime Format String

- Instance method `dt.strftime(format)` converts the `datetime` object into a string according to the given format.
- Class method `datetime.datetime.strptime(string, format)` parses a string into a `datetime` object using the given corresponding format.

The format codes as below:

| Directive | Meaning |
|-----------|---------|
| `%Y`      | Year with century
| `%y`      | Year without century (1970 to 2069)
| `%m`      | Month as a decimal number
| `%B`      | Full month name
| `%b`      | Abbreviated month name
| `%d`      | Day of the month
| `%j`      | Day of the year
| `%w`      | Day of the week, Sunday as `0`
| `%A`      | Full weekday name
| `%a`      | Abbreviated weekday name
| `%H`      | Hour (24-hour clock)
| `%I`      | Hour (12-hour clock)
| `%M`      | Minute
| `%S`      | Second
| `%p`      | `AM` or `PM`
| `%%`      | Literal `%` character


## Multithreading

Python programs by default have a single thread of execution, and will not terminate until all its threads have terminated.

### Threads

The **`threading` module** offers ways to create and manage separate threads through the `Thread` class.

**Instantiate**

`threading.Thread(target=None, name=None, args=(), kwargs={})` returns a `Thread` object. Parameters:

- _target_ is a callable as the target to be run.
- _name_ is the given thread name to override the by default constructed unique thread name.
- _args_ and _kwargs_ are to be passed to the target.

**Start**

`thread.start()` creates a new thread and starts executing the target function in the new thread according to the `Thread` object.

**Join**

`thread.join(timeout=None)` blocks the calling thread, and waits until the thread whose `join()` method is called terminates or the optional timeout occurs.

### Timers

`Timer` is a subclass of `Thread` and represents an action that should be run only after a certain amount of time has passed.

**Instantiate**

`threading.Timer(interval, target, args=(), kwargs={})` returns a `Timer` that will run _target_ with _args_ and _kwargs_, after _interval_ seconds.

**Cancel**

`timer.cancel()` stops the timer, and cancels the execution of the target if the timer is still in its waiting stage.

### Locks

The **`threading` module** comprises the `Lock` class implementing primitive lock objects.

**Instantiate**

`threading.Lock()` returns a primitive lock object. Its methods are executed atomically.

**Acquire**

`lock.acquire(blocking=True, timeout=-1)` acquires a lock. I.e., if the lock is unlocked, set it to locked and return `True`; otherwise:

- If _blocking_ is `True`, block for at most the number of seconds specified by the positive floating-point _timeout_ until the lock is unlocked;
- If _blocking_ is `False`, return `False` immediately.

**Release**

`lock.release()` releases a lock. I.e., if the lock is locked, reset it to unlocked; otherwise, raise `RuntimeError`.

If any other threads are blocked waiting for the lock to become unlocked, allow exactly 1 of them to proceed. Can be called from any thread.

**Status**

`lock.locked()` returns `True` if the lock is acquired, or `False` otherwise.

### Reentrant Locks

The **`threading` module** comprises the `RLock` class implementing reentrant lock objects.

**Instantiate**

`threading.RLock()` returns a reentrant lock object that may be acquired multiple times by the same thread.

**Acquire**

`lock.acquire(blocking=True, timeout=-1)` acquires a lock. If this thread owns the lock, increment the recursion level by 1 and return `True`.

**Release**

`lock.release()` releases a lock. If the recursion level is 0, reset the lock to unlocked; else decrement the recursion level by 1.

Can only be called from the thread that owns the lock, or a `RuntimeError` will be raised.

### Condition Variables

A condition variable is typically used to monitor a state with common interests. It allows one or more threads to wait until they are notified.

**Instantiate**

`threading.Condition(lock=None)` returns a condition variable object. A given _lock_ or a newly created `RLock` is used as the underlying lock.

**Lock**

A condition variable is always associated with a lock. Thus `acquire(*args)` and `release()` methods will act on the underlying lock.

**Wait**

1. `cond.wait(timeout=None)` releases the underlying lock, and then blocks and waits until notified and awaken, or until a timeout occurs.
Once awakened or timed out, it re-acquires the lock and returns `True` unless a given timeout expired.
2. `cond.wait_for(predicate, timeout=None)` waits until a callable _predicate_ evaluates to true, or until a timeout occurs.
It returns the last return value of the predicate.

Raise `RuntimeError` if the calling thread has not acquired the lock when this method is called.

**Notify**

1. `cond.notify(n=1)` wake up at most _n_ of the threads waiting on this condition, but does not actually release the lock.
2. `cond.notify_all()` wakes up all threads waiting on this condition, but does not actually release the lock.

Raise `RuntimeError` if the calling thread has not acquired the lock when this method is called.

### Semaphores

The **`threading` module** comprises the `Semaphore` class and `BoundedSemaphore` class implementing semaphore objects.

**Instantiate**

1. `threading.Semaphore(value=1)` returns a semaphore object. A semaphore manages an atomic counter whose value is: _value_ - `P()` + `V()`.
2. `threading.BoundedSemaphore(value=1)` returns a bounded semaphore object. It guarantees the current value never exceeds its initial value, or raises `ValueError`.

**Wait**

`sem.acquire(blocking=True, timeout=None)` acquires a semaphore. I.e., if the counter is larger than 0, decrement it by 1 and return `True`; or:

- If _blocking_ is `True`, block for at most the number of seconds optionally specified by the positive floating-point _timeout_ until awoken;
- If _blocking_ is `False`, return `False` immediately.

**Signal**

`sem.release(n=1)` releases a semaphore. I.e., increment the internal counter by _n_.

When it was 0 on entry and other threads are waiting to be awoken, wake up _n_ of those threads.

### Context Managers

Objects provided by the `threading` module with `acquire()` and `release()` methods can serve as context managers for a **`with` statement**.

- When entering the `with` block, the `acquire()` method will be called;
- When exiting the `with` block, the `release()` method will be called.


## *Examples*

**Stopwatch**

```python
import time

print('Press ENTER to begin or take a lap. Press Ctrl-C to quit.')
input()
print('Starting...')
timestamp = time.time()
count = 0
total = 0.00

try:
    while True:
        input()
        lap = time.time() - timestamp
        total += lap
        count += 1
        print(f'Lap #{count}: {round(total, 2)} ({round(lap, 2)})', end='')
        timestamp = time.time()
except KeyboardInterrupt:
    print('\n\Terminated.')
```

**Task Scheduler**

```python
import time, datetime, threading
def timer(days=0, hours=0, minutes=0, seconds=0):
    interval = datetime.timedelta(
        days = days,
        hours = hours,
        minutes = minutes,
        seconds = seconds
    )
    appointment = datetime.datetime.now() + interval
    def decorator(func):
        def wrapper(*args, **kwargs):
            while datetime.datetime.now() < appointment:
                time.sleep(1)
            func(*args, **kwargs)
        return lambda *args, **kwargs: threading.Thread(
            target = wrapper,
            args = args,
            kwargs = kwargs
        )
    return decorator

@timer(seconds = 5)
def hello(msg):
    print(msg)

hello('Greetings from the Earth!').start()
```


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
