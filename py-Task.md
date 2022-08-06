# Python Task Management


###### _Table of Contents_

- Command Line Arguments
- Time
	1. Timestamp
	2. Datetime
	3. Timedelta
	4. Datetime String
- Multithreading
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

The **`threading` module** offers ways to create and manage separate threads through the `Thread` objects.

**Instantiation**

`threading.Thread(target=None, name=None, args=(), kwargs={})` returns a `Thread` object.
_target_ is a callable as the target to be run.
_name_ is the given thread name to override the by default constructed unique thread name.
_args_ and _kwargs_ are to be passed to the target.

**Start**

`thread.start()` creates a new thread and starts executing the target function in the new thread according to the `Thread` object.

**Join**

`thread.join(timeout=None)` blocks the calling thread, and waits until the thread whose `join()` method is called terminates or the optional timeout occurs.


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


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
